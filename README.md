# Notes on C++

***Contents***
 - C++20 Ranges Library.
 - C++20 Random Library.
 - C++ Alignas Specifier.
 - Useful Links.
 - Input/Output Manipulators.
 - String Literals.
 - std::containers

**C++20 Ranges Library**

Using the c++20 ranges library, you can do things like this:
```C++
std::vector<int> vec{1, 2, 3, 4};
auto x = vec | std::views::take(2);
```
and
```C++
auto print(auto& x) {for(auto _ : x) {std::cout << _ << ", ";} }
print(coll1 | std::views::take(3)); 
```
These are included in the `ranges` header file, for both ranges and views.



**C++ Random Library**

For random numbers, you can use `std::random_default_engine`, you initialize `std::random_default_engine` with `std::random_device{}}()`. There is also `std::uniform_int_distribution` that you can pass a range of numbers in like: `1 - 99`. Here is an example implementation of a random function using the standard random library:
```C++
emplate <typename T>
void randomAdd(T& vals)
{ 
std::default_random_engine dre{std::random_device{}()};
std::uniform_int_distribution random{1,99};
for (auto& v : vals) { // add random value to each elem
v += random(dre);
}
}
```
- `std::default_random_engine`
      ¬ `std::random_device`
            ¬ `std::default_random_engine dre{std::random_device{}()};`
- `std::uniform_int_distribution`
      ¬ initialize with a range of values: e.g. `1 - 99`
             ¬ `std::uniform_int_distribution random{1,99};`
       
**C++ Alignas specifier**

With the C++ alignas specifier you can choose what the alignment of something will be.

Here are some examples:
```C++
struct alignas(64) container {char buff[24]{};} // alignof(container) == 64
int alignas(16) c{};                            // alignof(c) == 16
```
In the `_` part of `alignas(_)` that is what the aligned type will be. Bear in mind that they all have to be powers of two. You can check how much that variable/container is aligned to by using the `alignof` key word.

**Input/Output Manipulators**
In c++ there are the usual input and output streams like `std::cout` and `std::cin`. Although you can do: `std::cout << something;` you can also do `std::cout.write(something, strlen(something))` where `something` is `const char* something {"Hello There\n"};`.
```C++
int something_one = 42;
std::cout << something_one;

const char something {"Hello There\n"};
std::cout.write(something, strlen(something));
```
You can flush iostreams using the `flush()` meber function, or it does it automatically with `std::endl` that is why you shouldn't use `std::endl` becuase it flushes the output buffer when it is unneccessary. Here is an example:
```C++
std::cout << "Hello World";
std::cout.flush();
```
We can also handle output errors using member functions like: `.good()`, `.fail()`, operator! `!std::cout`, `.exeptions()`. Here is an example using these.
```C++
if(std::cout.good())
{
  std::cout << "All Good\n";
}

if(std::cout.fail())
{
  std::cout << "Not All Good.\n";
}

if(!std::cout)
{
  std::cout << "Do something in response\n";
}

try
{
std::cout << "Hello World\n";
} catch(const std::ios_base::failure& ex)
{
  std::cerr << "Caught exception: " << ex.what() << ", error code: " << ex.code() << "\n";
}
```
With `std::cin` you can also do, `while(std::cin >> x)` and then you can perform operations on x. An example impolementation using this, looks like this:
```C++
while(std::cin >> x)
{
  if(std::isdigit(ch))
  {
    cin.unget()
  }
    else
    {
      // do something else.
    }
}
```
`getline` is a very useful thing in the iostreams library. You can get a whole line of input using it:
```C++
std::string s{};
getline(std::cin, s);
```
Filestreams are also very important in the standard library, you can use a file by doing `std::ofstream` or `std::ifstream` depending on if you are going to read or write to the file. Here is an example of using this:
```C++
std::ifstream inFile{"input.txt"};
std::ostream outFile{"output.txt"};

outFile << "Hello There!";

std::string StringToken;
inFile >> StringToken;
```

**String Literals**
You can overload the `operator""` for string literals, an example is like this:
```C++
auto operator""_sec(long double i)
{
  return Second{static_cast<int>(i)};
}
```
Notice the function has to accept a long double.

**std::containers**

`std::map` looks like this:
```C++
map<int, int> {{10, 20}, {30, 40}};
```

**Useful Links**

- https://meetingcpp.com/mcpp/slides/2022/MeetingC++_C++20_BelleViews_Keynote_josuttis_2211178984.pdf



