## Generics in TypeScript and Asynchronous Promises.

# Introduction
Generics allow developers to write reusable functions, interfaces, and
classes while preserving type information. Instead of fixing a function
to one data type, a generic function can work with different types
safely. Generics are especially useful when handling asynchronous
operations that return Promise values.

# Detailed Explanation
A generic type parameter is commonly written as <T>. TypeScript infers
the actual type from the supplied argument or accepts it explicitly.
function getFirst<T>(items: T[]): T | undefined {
  return items[0];
}

const firstName = getFirst(["Mina", "Rafi"]);
const firstNumber = getFirst([10, 20, 30]);
In the first call, TypeScript infers T as string; in the second, it
infers T as number. The function therefore returns the correct value
type without using any.

A Promise<T> describes a promise that will fulfill with a value of
type T. For example:
async function getUser(): Promise<{ id: number; name: string }> {
  const response = await fetch("/api/user");
  if (!response.ok) {
    throw new Error("Could not load user");
  }
  return response.json();
}
Here, Promise<{ id: number; name: string }> documents the expected
successful result. The async keyword makes the function return a
promise, while await waits for that promise to settle. A generic API
helper can also preserve the response type:
async function fetchData<T>(url: string): Promise<T> {
  const response = await fetch(url);
  if (!response.ok) throw new Error("Request failed");
  return response.json() as Promise<T>;
}

type Product = { id: number; title: string };
const product = await fetchData<Product>("/api/product");
The caller supplies Product as the expected data type. This type
describes what the application expects; it does not validate untrusted
server data at runtime.

# Conclusion
Generics make asynchronous code reusable and strongly typed. Combined
with Promise<T>, they help developers describe the expected result of
an operation and catch type mistakes during development.