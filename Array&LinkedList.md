#JAVA数据结构 day1
---
##数组与单链表
---
####数组:有限个相同类型变量的有序集合
**数组的基本操作**

`读取元素`
```
//给定数组
int [] arr = new int []{1,2,3};
public static void main (String [] args){
	System.out.print(arr[2]);
}
```
`更新元素`
```
int [] arr = new int []{1,2,3};
public static void main (String [] args){
		arr[2]=9;
	System.out.print(arr[2]);
}
```
`插入元素`
```
//尾部插入
//若数组仍有空闲位置即可按照更新操作插入
   arr[2]=8;
```
```
//中间插入
public class MidInsert {
    private int [] arr;
    private int size;

    public void InitArr(int length){
        this.arr=new int[length];
        size=0;
    }
    public void Insert(int item, int index) throws Exception{
        //detect if index out of range
        if(index < 0 || index>size){
            throw new IndexOutOfBoundsException("index out of range!");
        }
        for(int i=size-1;i>=index;i--){
            arr[i+1]=arr[i];
        }
        arr[index]=item;
        size++;
    }
    public void output(){
        for(int i=0;i<size;i++){
            System.out.print(arr[i]+"\n");
        }
    }
}
```
```
//数组扩容
    public void resize(){
        int[] arrNew = new int[arr.length*2];
        System.arraycopy(arr,0,arrNew,0,arr.length);
        arr=arrNew;
    }
```
`删除元素`
```
//类似插入的反向操作
    public int delete(int index) throws Exception{
        if(index < 0 || index>=size){
            throw new IndexOutOfBoundsException("out of bound");
        }
        int delItem = arr[index];
        for(int i=index;i<size-1;i--){
            arr[i]=arr[i+1];
        }
        size--;
        return delItem;
    }
```
------
####链表
>linked list：在物理上非连续、非顺序的数据结构，由若干节点组成。
>存储方式：随机存储
>单向链表：每一个节点包含两个部分，一部分是存放数据的变量data，另一部分是指向下一节点的指针next。
```
private static class Node{
int data;
Node next;
}
```
>双向链表：相较于单向链表，多了一个指向前置节点的prev指针
```
private static class BiNode{
int data;
Node next;
Node prev;
}
```
---
`链表示例`
```
package com.company;


public class LinkedList {
    /**
     *链表结构
     */
    private static class Node{
        int data;
        Node next;
        Node (int data){
            this.data=data;
        }
    }
    private Node head;
    private Node last;
    private int size;
    
    /**
     *插入数据
     */
    public void  insert(int data, int index)throws Exception{
        if(index<0||index>=size){
            throw new IndexOutOfBoundsException("out of bound!");
        }
        Node insertedNode = new Node(data);
        if(size==0){
            head=insertedNode;
            last=insertedNode;
        }else if(index==0){
            insertedNode.next=head;
            head=insertedNode;
        }else if(size==index){
            last.next=insertedNode;
            last=insertedNode;
        }else {
            Node prevNode=get(index-1);
            insertedNode.next=prevNode.next;
            prevNode.next=insertedNode;
        }
        size++;
    }
    
    /**
     *删除节点
     */
    public Node remove(int index) throws Exception{
        if(index<0 || index>=size){
            throw new IndexOutOfBoundsException("out of bound!");
        }
        Node delItem=null;
        if(index==0){
            delItem=head;
            head=head.next;
        }else if(index==size-1){
            Node prevNode=get(index-1);
            delItem=prevNode.next;
            prevNode.next=null;
            last=prevNode;
        }else {
            Node prevNode=get(index-1);
            Node nextNode=prevNode.next.next;
            delItem=prevNode.next;
            prevNode.next=nextNode;
        }
        size--;
        return delItem;
    }
    
    /**
      *查找元素位置
      */
    public Node get(int index) throws Exception{
        if (index<0||index>=size){
            throw new IndexOutOfBoundsException("out of bound!");
        }
        Node temp = head;
        for (int i =0;i<index;i++){
            temp=temp.next;
        }
        return temp;
    }
    
    /**
     *输出链表
     */
    public void output(){
        Node temp = head;
        while(temp!=null){
            System.out.print(temp.data);
            temp=temp.next;
        }
    }
}

```
