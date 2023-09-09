---
tags:
  - java
  - polymorphism
---
```java
// parent class
class Order{  
  
	int id;  
	String name;  
	Order(int id, String name){  
		this.id = id;  
		this.name = name;  
	}  
	  
	public String toString(){  
		return "Order id: " + id + ", " + " Order name: " + name;  
	}  
} 
// child class
class Product extends Order{  
	int id;  
	String name;  
	Product(int id, String name){  
		super(id, name);  
		this.id = id;  
		this.name = name;  
	}  
	  
	public String getId(){  
		return "Product id: " + this.id;  
	}  
	  
	  
	public String toString(){  
		return "Product id: " + id + ", " + "Product name: " + name;  
	}  
}  
  
  
public class Main {  
	public static void main(String[] args) {  
	Order o1 = new Product(1, "Ice Cream");  
	// Can only see order object methods, so this does not work
	/* ---> System.out.println("via order reference: " + o1.getId()); */
	// Can see Product / Children method due to polymorphism. Same method exists in Order object and Product object  
	// In order to see child methods we can cast the object and then call  
	System.out.println("toString via order reference: " + o1);
	if (o1 instanceof Product){  
			Product p1 = (Product) o1;  
			System.out.println(p1.getId());  
		}    
	}  
}
```