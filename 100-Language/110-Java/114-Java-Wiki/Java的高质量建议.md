避免自增陷阱
int count = 0;  
for (int i = 0; i < 10; i++) {  
    count = count++;  
}  
System.out.println(count);

