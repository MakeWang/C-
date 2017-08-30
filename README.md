# C语言文件操作
## 目录<br/>
* [读取文件](#读取文件)
* [写文件](#写文件)
* [读写二进制文件](#读写二进制文件)
* [计算文件大小](#计算文件大小)
* [文件加解密](#文件加解密)
* [二进制加解密](#二进制加解密)
    
#### 读取文件
----------------------------------------------------
```java
int main(){
	char *file_path = "E:\\java(Android)加密AESOperator类.txt";
	FILE *fp = fopen(file_path,"r");
	
	char buff[50];
	//读取字字符串
	while (fgets(buff, 50, fp)){
		printf("%s",buff);
	}
	//读取一个字符
	//int c = fgetc(fp);
	//printf("%c", c);
	fclose(fp);
	getchar();
	return 0;
}
```

#### 写文件
----------------------------------------------------
```java
int main(){
	char *file_path = "E:\\test.txt";
	FILE *fp = fopen(file_path, "w");
	char *content = "你好。我来了！";
	fputs(content, fp);
	fclose(fp);
	getchar();
	return 0;
}
```

#### 读写二进制文件
----------------------------------------------------
```java
int main(){
	char *file_r = "E:\\FlycoTabLayout-master.zip";
	char *file_w = "E:\\FlycoTabLayout-master2.zip";
	FILE *fp_r = fopen(file_r,"rb");
	FILE *fp_w = fopen(file_w, "wb");
	char buff[50];
	int len = 0;

	while ((len = fread(buff, sizeof(char),50, fp_r)) != 0){
		fwrite(buff, sizeof(char), len, fp_w);
	}
	fclose(fp_r);
	fclose(fp_w);
	system("pause");
	return 0;
}
```
#### 计算文件大小
----------------------------------------------------
```java
int main(){

	char *file_r = "E:\\FlycoTabLayout-master.zip";
	FILE *fp_r = fopen(file_r, "r");
	if (fp_r == NULL){
		return 0;
	}
	fseek(fp_r, 0, SEEK_END);
	long size = ftell(fp_r);
	printf("%d \n",size);
	fclose(fp_r);
	system("pause");
	return 0;
}
```
#### 文件加解密
----------------------------------------------------
```java
//加密
int encode(char path[],char path_encode[]){
	FILE * normal_fp = fopen(path, "r");
	FILE * encode_fp = fopen(path_encode, "w");

	int ch;
	while ((ch = fgetc(normal_fp)) != EOF){
		fputc(ch ^ 7, encode_fp);
	}
	fclose(normal_fp);
	fclose(encode_fp);
	return 0;
}
//解密
int decode(char path_encode[], char path_decode[]){
	FILE * normal_fp = fopen(path_encode, "r");
	FILE * encode_fp = fopen(path_decode, "w");

	int ch;
	while ((ch = fgetc(normal_fp)) != EOF){
		fputc(ch ^ 7, encode_fp);
	}
	fclose(normal_fp);
	fclose(encode_fp);
	return 0;
}
int main(){
	char *file_path = "E:\\java(Android)加密AESOperator类.txt";
	char *file_path_encode = "E:\\java(Android)加密AESOperator类2.txt";
	char *file_path_decode = "E:\\java(Android)加密AESOperator类3.txt";
	//加密
	//encode(file_path, file_path_encode);
	//解密
	decode(file_path_encode,file_path_decode);
	system("pause");
	return 0;
}
```

#### 二进制加解密
----------------------------------------------------
```java
//加密
int encode(char path[],char path_encode[],char *password){
	FILE * normal_fp = fopen(path, "rb");
	FILE * encode_fp = fopen(path_encode, "wb");

	int ch;
	int pwd_legth = strlen(password);
	int i = 0;
	while ((ch = fgetc(normal_fp)) != EOF){
		fputc(ch ^ password[i*pwd_legth], encode_fp);
		i = (i++) % 10001;
	}
	fclose(normal_fp);
	fclose(encode_fp);
	return 0;
}
//解密
int decode(char path_encode[], char path_decode[], char *password){
	FILE * normal_fp = fopen(path_encode, "rb");
	FILE * encode_fp = fopen(path_decode, "wb");

	int ch;
	int pwd_legth = strlen(password);
	int i = 0;
	while ((ch = fgetc(normal_fp)) != EOF){
		fputc(ch ^ password[i*pwd_legth], encode_fp);
		i = (i++) % 10001;
	}
	fclose(normal_fp);
	fclose(encode_fp);
	return 0;
}

int main(){
	char *file_path = "E:\\h5.png";
	char *file_path_encode = "E:\\h51.png";
	char *file_path_decode = "E:\\h52.png";
	//加密
	encode(file_path, file_path_encode,"wangyin");
	//解密
	//decode(file_path_encode, file_path_decode, "wangyin");
	system("pause");
	return 0;
}
```


