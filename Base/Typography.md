2023-10-14 18:05
Tags: #

---
```tsx
import { ComponentPropsWithoutRef, ElementType, ReactNode } from 'react'

export type TypographyProps<T extends ElementType> = {
  as?: T
  variant?:
    | 'large'
    | 'h1'
    | 'h2'
    | 'h3'
    | 'body1'
    | 'subtitle1'
    | 'body2'
    | 'subtitle2'
    | 'caption'
    | 'overline'
    | 'link1'
    | 'link2'
  children?: ReactNode
  className?: string
} & ComponentPropsWithoutRef<T>
export const Typography = <T extends ElementType>({
  as,
  variant = 'body1',
  children,
  className,
  ...restProps
}: TypographyProps<T> & Omit<ComponentPropsWithoutRef<T>, keyof TypographyProps<T>>) => {
  const classNames = `${s[variant]} ${className}`
  const Component = as || 'p'

  return (
    <Component {...restProps}>
      {children}
    </Component>
  )
}
```

---
### Links
[[Компоненты]]