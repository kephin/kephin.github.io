# TypeScript with React

## Functional Component

- The easiest way is to create the props type
- Return type is inferred
- It's discourage to use `React.FC`

### Define a type for Props with children

```ts
// #1 ReactNode
import React, { type ReactNode } from "react";

type HeaderProps = {
  title: string;
  children: ReactNode;
};

export const Header = ({ title, children }: HeaderProps) => {
  return (
    <div>
      {title}
      {children}
    </div>
  );
};

// #2 PropsWithChildren
import React, { type PropsWithChildren } from "react";

type HeaderProps = PropsWithChildren<{ title: string }>;

export const Header = ({ title, children }: HeaderProps) => {
  return (
    <div>
      {title}
      {children}
    </div>
  );
};
```

## Hooks

```ts
// use inferred types
const [state, setState] = useState(false);

// many hooks are initialized with null-ish default values
const [user, setUser] = useState<User[] | null>(null);
```

## Pass setState as props

```ts
import { Dispatch, SetStateAction } from "react";

interface IProps {
  myVar: boolean;
  setMyVar?: Dispatch<SetStateAction<boolean>>;
}
```

## Form and Events

```ts
import { type FormEvent } from "react";

const NewGoal = () => {
  const handleSubmit = (event: FormEvent) => {
    event.preventDefault();
  };
};
```
