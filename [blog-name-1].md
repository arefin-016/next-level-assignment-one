## Type Aliases vs Interfaces in TypeScript
# Introduction
TypeScript provides both type aliases and interface declarations to
describe the shape of data. They often look similar, especially when
defining object properties. However, they have different capabilities,
and choosing the right one can make a codebase easier to maintain.

# Detailed Explanation
An interface is mainly designed to describe object structures. It can be
extended by another interface using extends, and it supports
declaration merging. Declaration merging means that TypeScript combines
multiple declarations with the same interface name.
interface User {
  name: string;
}

interface User {
  age: number;
}

const user: User = { name: "Arefin", age: 22 };
A type alias can describe an object, but it can also represent unions,
intersections, tuples, primitives, and other types. For example:
type Status = "pending" | "approved" | "rejected";

type Admin = {
  name: string;
  permissions: string[];
};

type Employee = Admin & {
  salary: number;
};
Both interfaces and type aliases can describe object properties and can
be extended or combined in different ways. An interface commonly uses
extends, while a type alias commonly uses the intersection operator
(&) to combine object types. Unlike interfaces, type aliases cannot be
reopened through declaration merging.

# When Should You Choose Each One?
Choose an interface when defining the public shape of an object or class
contract, especially when extension and declaration merging are useful.
Choose a type alias when defining unions, tuples, intersections, or more
complex type expressions. For ordinary object models, either option is
valid, so consistency across a project is important.

# Conclusion
Neither feature is universally better. Understand their differences,
then choose the one that communicates the intended structure most
clearly.