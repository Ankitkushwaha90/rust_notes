Object-Oriented Programming (OOP) in Rust can be approached through concepts like encapsulation, inheritance (via traits and trait objects), and polymorphism. Rust doesn’t have classes like traditional OOP languages but uses structs and traits to achieve similar functionality.

Here’s a breakdown of OOP concepts in Rust with examples:

### Table of Contents
- 1. Encapsulation with Structs and Methods
- 2. Inheritance with Traits
- 3. Polymorphism with Trait Objects
Example: A Simple Object-Oriented Program
### 1. Encapsulation with Structs and Methods
In Rust, we encapsulate data by defining structs and implementing associated methods with impl. Private fields are restricted by using the pub keyword.

Example: Defining a Struct with Methods
```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // Public method to calculate area
    fn area(&self) -> u32 {
        self.width * self.height
    }

    // Associated function to create a square
    fn square(size: u32) -> Rectangle {
        Rectangle { width: size, height: size }
    }
}

fn main() {
    let rect = Rectangle {
        width: 10,
        height: 20,
    };

    println!("The area of the rectangle is: {}", rect.area());

    let square = Rectangle::square(15);
    println!("The area of the square is: {}", square.area());
}
```
Here, area and square are methods of Rectangle. Only the methods themselves have access to the struct’s private fields (width and height).

### 2. Inheritance with Traits
Rust doesn’t have traditional inheritance. Instead, it uses traits, which are similar to interfaces in other languages. Traits allow us to define shared behavior that structs can implement.

Example: Creating Traits
```rust
trait Shape {
    fn area(&self) -> f64;
}

struct Circle {
    radius: f64,
}

impl Shape for Circle {
    fn area(&self) -> f64 {
        3.14 * self.radius * self.radius
    }
}

struct Rectangle {
    width: f64,
    height: f64,
}

impl Shape for Rectangle {
    fn area(&self) -> f64 {
        self.width * self.height
    }
}

fn main() {
    let circle = Circle { radius: 5.0 };
    let rect = Rectangle {
        width: 10.0,
        height: 20.0,
    };

    println!("Circle area: {}", circle.area());
    println!("Rectangle area: {}", rect.area());
}
```
In this example, both Circle and Rectangle structs implement the Shape trait, making it possible to define the area function for each shape without needing traditional inheritance.

### 3. Polymorphism with Trait Objects
Rust supports polymorphism through trait objects, which enable dynamic dispatch. We can use trait objects to create references to different struct types that share a common trait.

Example: Using Trait Objects for Polymorphism
```rust
trait Shape {
    fn area(&self) -> f64;
}

struct Circle {
    radius: f64,
}

impl Shape for Circle {
    fn area(&self) -> f64 {
        3.14 * self.radius * self.radius
    }
}

struct Rectangle {
    width: f64,
    height: f64,
}

impl Shape for Rectangle {
    fn area(&self) -> f64 {
        self.width * self.height
    }
}

fn print_area(shape: &dyn Shape) {
    println!("The area is: {}", shape.area());
}

fn main() {
    let circle = Circle { radius: 5.0 };
    let rectangle = Rectangle {
        width: 10.0,
        height: 20.0,
    };

    print_area(&circle);
    print_area(&rectangle);
}
```
Here, print_area accepts a reference to any type that implements the Shape trait. This allows polymorphic behavior since both Circle and Rectangle implement Shape.

### 4. Example: A Simple Object-Oriented Program
This example brings it all together by defining a trait for a Vehicle, with different implementations for a Car and a Bike.

Example: Defining a Vehicle Trait with Implementations for Car and Bike
```rust
trait Vehicle {
    fn drive(&self);
}

struct Car {
    make: String,
    model: String,
}

impl Vehicle for Car {
    fn drive(&self) {
        println!("Driving a car: {} {}", self.make, self.model);
    }
}

struct Bike {
    brand: String,
}

impl Vehicle for Bike {
    fn drive(&self) {
        println!("Riding a bike: {}", self.brand);
    }
}

// Function that accepts any vehicle type
fn start_trip(vehicle: &dyn Vehicle) {
    vehicle.drive();
}

fn main() {
    let car = Car {
        make: String::from("Toyota"),
        model: String::from("Corolla"),
    };

    let bike = Bike {
        brand: String::from("Schwinn"),
    };

    start_trip(&car);
    start_trip(&bike);
}
```
### In this example:

We define a Vehicle trait with a drive method.
Both Car and Bike structs implement the Vehicle trait.
We use a function start_trip that takes a reference to any Vehicle, enabling polymorphic behavior. This means we can pass either a Car or a Bike to start_trip, and it will call the appropriate drive method.
With Rust’s traits and struct-based approach, we achieve encapsulation, polymorphism, and code reuse without the need for traditional inheritance. This approach leads to flexible, efficient, and safe code that is aligned with Rust's philosophy of ownership and memory safety.
