2025-06-24 15:10
Tags: #performance



---

```ts
export const EnumStatus = {
	SUCCESS: "SUCCESS",
	ERROR: "ERROR",
	PENDING: "PENDING"
} as const

export type EnumStatus = (typeof EnumStatus)[keyof typeof EnumStatus]
```

---
### Links
[[React]]
