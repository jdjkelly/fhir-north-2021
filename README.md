## FHIR North 2021

* Presented in pre-recorded format on Wed Oct 13, 2021.
* [Slides available for download](https://github.com/jdjkelly/fhir-north-2021/files/7340389/SESAI3UWFHQW036EU_Building.on.FHIR.in.TypeScript.pdf)

Thanks to Brian Kaney and Gino Canessa for their work on making this possible.

# Building on FHIR with TypeScript

## Agenda

* [Why TypeScript?](#Why-Typescript?)
* [How to read TypeScript]()
* [How to use @types/fhir]()
* [Building a type-safe UI with FHIR and React]()

## Why TypeScript?

### What is TypeScript?

TypeScript has all of the same features of JavaScript with one important addition: a type system.

Types are the rules and interfaces for the data structures in the programs we write. JavaScript is a "dynamically typed" language. You don't even need to know about types to write it.

TypeScript adds its own type system as a layer on top of JavaScript.

### Why do we care about types?

* Runtime safety. We want to ship programs that work and run without bugs.
* Tool for thought and improving design. Understanding more about the structure of the data in our programs helps us understand our problem domain better.
* Common ground for collaboration between teams and groups. If multiple open source projects . Increased interoperability.

All three of these are available in other FHIR language communities like Java and C#.

## How to read TypeScript

```typescript
const name: string = "Josh"
```

```typescript
function(a: number, b: number): number {
  return a + b;
}
```

```typescript
interface Patient {
  resourceType: "Patient",
  id: string
}
```

## How to use @types/fhir

FHIR community members interested in using FHIR and JavaScript came together to create TypeScript definitions automatically from the FHIR JSON Schema release. 

You might not know this, but every release of FHIR ships with a JSON Schema that fully describes all of the Resources in the standard. We use that JSON Schema file to generate code for us in whatever languages we need. So far, fhir-codegen ships C# and TypeScript code. It reads the JSON Schema into an Abstract Syntax Tree, and then we print out the appropriate syntax for the TypeScript output.

### Installing

There are just 2 steps:

1. Install TypeScript and @types/fhir in a new project
2. Adding a TypeScript config file

You can also clone this template: https://github.com/jdjkelly/fhir-typescript-template

```
npm i typescript @types/fhir --save-dev
npx tsc --init
```

### Usage basics

#### Annotating a variable

```typescript
import { Patient } from "fhir/r4"

const patient: Patient = {
  resourceType: "Patient",
  id: "1234-123-1234-123"
}
```

#### Namespace support

In tsconfig.json add:

```json
   "types": ["fhir"]
```

Now, we have access to fhir2, fhir3, and fhir4 as global scoped types available to us everywhere (including in the following examples).

#### Use with a function

```typescript
const isPatient = (resource: fhir4.Resource): resource is fhir4.Patient => {
  return resource.resourceType === 'Patient'
}
```

#### Use with Fetch

```typescript
const isPatient = (resource: fhir4.Resource): resource is fhir4.Patient => {
  return resource.resourceType === 'Patient'
}

const request = await fetch("http://hapi.fhir.org/baseR4/Patient/1274805")

const patient: fhir4.Patient = request.json()

if (isPatient(request.json()) {
  console.dir(res, {depth: 4 })
}
```

## Building a type-safe UI with FHIR and React

```
npx create-react-app my-app --template typescript
npm install --save-dev @types/fhir
```
