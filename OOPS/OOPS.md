1. setter/getter -> function used to access private attributes
 - ![[Screenshot_2024-07-28-10-58-54-498_org.videolan.vlc.jpg]]
 - Learn all the definitions of the 4 pillars of oops.
 - 1. Encapsulation: data/properties + member functions combine to form a class. So, encapsulation is wrapping up of data & member functions together to form a class.
    - Helps in data hiding (using private access modifier) like bank balance / password etc
    - 
 - ### Constructor
   - invoked automatically at the time of ==object creation.== Like in class DSU, when we write in main function Dsu a(n). Here, its the constructor.
   - either programmer makes constructor, or the compiler 
   - #### constructor overloading
     - multiple constructions in the class having same name but different types
     - It is an example of **polymorphism
     - Non parameterized, parameterized, copy constructor 
     - this constructor :
      - ![[Screenshot_2024-07-29-07-58-53-628_org.videolan.vlc.jpg]]
      - ![[Screenshot_2024-07-29-08-00-11-690_org.videolan.vlc.jpg]]
    - Copy constructor: To copy properties of object into another.
      - ![[Screenshot_2024-07-29-08-03-50-057_org.videolan.vlc.jpg]]
      - ![[Screenshot_2024-07-29-08-20-48-423_org.videolan.vlc.jpg]]
- #### Destructor
	- To deallocate the space
	- ~Student(){
	  }
	- Destructor is also called automatically

- # Inheritance
	- ![[Pasted image 20240730181234.png]]
	- Person is base class, Student is derived class
	- 