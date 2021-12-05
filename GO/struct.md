# struct

```go
package main

import (
 "fmt"
 "unsafe"
)

func main() {
 diff()

 // 结构体 struct
 type InitStruct struct {
  name   string
  age    int
  gender bool
 }
 type Struct struct {
  name, hobby string
  age         int
  gender      bool
 }

 // 结构体实例化
 type Person struct {
  name, hobby string
  age         int
  gender      bool
 }
 var jokereven Person
 fmt.Println(jokereven)

 // 匿名结构体
 var user struct {
  name string
  age  int
 }
 user.name = "jokereven"
 user.age = 19

 // 创造指针类型结构体
 var joker = new(Person)
 fmt.Printf("type of the joker:%T\n", joker) //type of the joker:*main.Person
 fmt.Printf("joker=%#v\n", joker)            //joker=&main.Person{name:"", hobby:"", age:0, gender:false}
 // Go支持对结构体指针使用.
 var even = new(Person)
 even.name = "even"

 // 取结构体的地址实例化
 kiku := &Person{}
 fmt.Printf("type of the kiku:%T\n", kiku) //type of the kiku:*main.Person

 // 结构体初始化
 var p Person
 // 没进行初始化的结构体的初始值的为0
 fmt.Printf("p=%#v\n", p) //p=main.Person{name:"", hobby:"", age:0, gender:false}

 // 使用键值对进行初始化
 // 对结构体进行初始化
 p1 := Person{
  name: "jokereven",
  age:  19,
 }
 fmt.Printf("p1=%#v\n", p1)
 // 对结构体指针进行初始化
 var p2 = &Person{
  name: "jokereven",
  age:  19,
 }
 fmt.Printf("p2=%#v\n", p2)
 // 使用值的列表进行初始化

 // 必须全部都写
 p3 := Person{
  "jokereven", "打代码",
  19,
  true,
 }
 fmt.Printf("p3=%#v\n", p3)

 // struct结构体内存布局
 type test struct {
  a int
  b int
  c int
  d int
 }
 var n = test{
  1, 2, 3, 4,
 }
 fmt.Printf("n.a %p\n", &n.a)
 fmt.Printf("n.b %p\n", &n.b)
 fmt.Printf("n.c %p\n", &n.b)
 fmt.Printf("n.d %p\n", &n.d)

 // 空结构体
 var v struct{}
 fmt.Println(unsafe.Sizeof(v)) // 0

 // 构造函数
 p4 := newPerson("jokereven", "杭州", 19)
 fmt.Println(p4)
 p4.Dream()

 // 方法和接收者
 /*
    func (接收者变量 接收者类型) 方法名(参数列表) (返回参数) {
      函数体
  }
 */
 fmt.Println(p4.age) // 19
 p4.SetAge1(20)
 fmt.Println(p4.age) //20
 // 值类型接受者 是把拷贝过来的副本给修改了so
 p4.SetAge2(21)
 fmt.Println(p4.age) //20
 /*
  什么时候应该使用指针类型接收者
  需要修改接收者中的值
  接收者是拷贝代价比较大的大对象
  保证一致性，如果有某个方法使用了指针接收者，那么其他的方法也应该使用指针接收者。
 */

 // 任意类型添加方法
 var m MyInt
 m.SayHello()
 m = 996
 fmt.Printf("type of the m:%v\n", m)
 fmt.Printf("m=%#v\n", m)

 // 结构体的匿名字段
 type instant struct {
  string
  int
 }
 i1 := instant{
  "jokereven",
  19,
 }
 fmt.Println(i1)

 // 嵌套结构体
 type country struct {
  name  string
  level int
 }
 type planet struct {
  country country
  size    int
 }
 plan := planet{
  country: country{
   name:  "china",
   level: 996,
  },
  size: 1024,
 }
 fmt.Println(plan)

 d := Dog{
  Feet: 4,
  Animal: &Animal{
   name: "jokereven",
  },
 }
 d.wang()
 d.Move()
}

// MyInt 自定义类型
type MyInt int

// SayHello 自定义类型的自定义方法
func (m MyInt) SayHello() {
 fmt.Println("my type is int")
}

func diff() {
 // 自定义类型
 type CustomType int
 // 类型别名
 type AliasName = int
 // 类型定义和类型别名的区别
 var custom CustomType
 var alias AliasName
 fmt.Printf("type of the custom:%T\n", custom) // type of the custom:main.CustomType
 fmt.Printf("type of the alias:%T\n", alias)   //type of the alias:int
}

type person struct {
 name string
 city string
 age  int8
}

// 构造函数
func newPerson(name, city string, age int8) *person {
 return &person{
  name: name,
  city: city,
  age:  age,
 }
}

func (p person) Dream() {
 fmt.Println(p.name)
}

// 指针类型接收者
func (p *person) SetAge1(newAge int8) {
 p.age = newAge
}

// 值类型接收者
func (p person) SetAge2(newAge int8) {
 p.age = newAge
}

// Animal 结构体的继承
type Animal struct {
 name string
}

// Move 动物
func (a *Animal) Move() {
 fmt.Printf("my name is %s\n", a.name)
}

// Dog 狗
type Dog struct {
 Feet    int
 *Animal //通过嵌套结构体实现继承
}

func (d *Dog) wang() {
 fmt.Printf("%s can 汪\n", d.name)
}
```
