```java
package com.sean.javaio;

import java.io.*;

/**
 * @author Yunxiong
 * @version 1.0
 * @date 11/22/2020
 */
public class FileOperation {
    public static void main(String[] args) throws IOException {
        //1. 创建文件
        createFile();
        //3. 创建文件夹
        createFileFolder();
        //4. 列出指定目录的全部文件
        listAllFiles();
        //5. 使用RandomAccessFile写入文件
       // useRandomAccessFile();
        //6. 向文件中写入字符串
        writeStringToFile();
        //7. 向文件中追加新内容
        appendStringToFile();
        //8. 读取文件内容
        readFileContent();
        //2. 删除文件
        deleteFile();
    }

    static void createFile() throws IOException {
        File file = new File("D:\\hello.txt");
        file.createNewFile();
    }

    static void deleteFile() {
        String fileName = "D:" + File.separator + "hello.txt";
        File file = new File(fileName);
        if (file.exists()) {
            file.delete();
        }
        // 删除文件夹
        /*String fileFolderPath = "D:" +File.separator + "fileDir" + File.separator + "fileDir2";
        File fileFolder = new File(fileFolderPath);
        if(fileFolder.isDirectory()){
            fileFolder.delete();
        }*/
    }

    static void createFileFolder() {
        String filePath = "D:" + File.separator + "fileDir" + File.separator + "fileDir2";
        File file = new File(filePath);
        //file.mkdir(); // 只能创建父目录存在的文件夹
        file.mkdirs();// 可以先创建不存在的父目录，再创建真正的文件夹
    }

    static void listAllFiles() {
        String filePath = "D:" + File.separator + "apache-maven-3.6.0";
        File file = new File(filePath);
        if (file.isDirectory()) {
            File[] files = file.listFiles();
            for (File fileObject : files) {
                System.out.println(fileObject);
            }
            /*for (int i = 0; i < files.length; i++) {
                System.out.println(files[i]);
            }*/
        }
    }

    static void useRandomAccessFile() throws IOException {
        String filePath = "D:" + File.separator + "hello.txt";
        File file = new File(filePath);
        RandomAccessFile randomAccessFile = new RandomAccessFile(file, "rw");

        randomAccessFile.writeChar('A');
        randomAccessFile.writeChars("this is randomAccessFile");

        randomAccessFile.close();
    }

    static void writeStringToFile() throws IOException {
        // 准备好需要写出去的内容
        String outContent = "这里是我需要写出到文件的内容！ sean 20201122 ";

        // 准备写出到哪个文件里面
        String fleName = "D:" + File.separator + "hello.txt";
        File file = new File(fleName);
        FileOutputStream out = new FileOutputStream(file);

        // 写出去前，需要把内容换成字节
        byte[] outContentBytes = outContent.getBytes();

        out.write(outContentBytes);
        out.close();
    }

    static void appendStringToFile() throws IOException {
        // 准备好需要追加的内容
        String appendContent = "==>这里是追加的内容！ 20201122";
        // 追加到哪个文件

        String fleName = "D:" + File.separator + "hello.txt";
        File file = new File(fleName);
        // true 表示是否追加，默认 false
        FileOutputStream out = new FileOutputStream(file, true);

        byte[] bytes = appendContent.getBytes();

        out.write(bytes);
        out.close();
    }

    static void readFileContent() throws IOException {
        String fileName = "D:" + File.separator + "hello.txt";
        File file = new File(fileName);
        FileInputStream in = new FileInputStream(file);
        byte[] readBytes = new byte[1024];

        int count = 0;
        int temp = 0;
        // -1 表示文件最后一行
        while((temp = in.read()) != (-1)){
            // 把临时读取到的放到byte数组中
            readBytes[count++] = (byte) temp;
        }
        in.close();
        System.out.println(new String(readBytes));

    }
}

```
