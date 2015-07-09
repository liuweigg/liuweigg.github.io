---
layout: post
title: 使用两个线程交替打印
category: 技术
tags: 多线程
keywords: 
description: 
---

好吧，这么简单的面试题，当时面试的时候居然写不出来——两个线程，一个线程打印1，一个线程打印a，打印数量不断增加，效果是1aa111aaaa...

	package lw.com;

	public class MainAndSubThread {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		final PrintMethod pm = new PrintMethod();
		
		
		Thread thread1 = new Thread(){
			public void run(){
				//for(int i = 0 ; i < 5 ; i ++ ){
				while(true){
					pm.printNum();
				}
			}
		};
		
		thread1.start();
		
		Thread thread2 = new Thread(){
			public void run(){
				//for(int i = 0 ; i < 5 ; i ++ ){
				while(true){
					pm.printString();
				}
			}
		};
		
		Thread2.start();
	  }
  	}

	class PrintMethod{
	private int num = 1 ;
	
	public synchronized void printNum(){
		for(int i = 0 ; i < num ; i ++ ){
			System.out.print(1);
		}
		num ++ ;

		try {
			this.notifyAll();
			this.wait();
			Thread.sleep(1000); 
		} catch (InterruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
	
	public synchronized void printString(){
		for(int i = 0 ; i < num ; i ++ ){
			System.out.print("a");
		}
		num ++ ;
		

		try {
			this.notifyAll();
			this.wait();
			Thread.sleep(1000); 
		} catch (InterruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		}
  	}

