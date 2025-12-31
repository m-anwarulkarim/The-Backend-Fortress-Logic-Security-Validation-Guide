# Express Request টাইপ বাড়ানো (req.user টাইপ ডিক্লেয়ার)\_

**কেন এটি করা হয়?**

- Express-এর ডিফল্ট Request অবজেক্টের মধ্যে user নামে কোনো প্রপার্টি থাকে না। কিন্তু যখন অথেন্টিকেশন মিডলওয়্যার (Authentication Middleware) ব্যবহার করা হয় , তখন টোকেন ভেরিফাই করার পর ইউজারের তথ্য req.user এ রাখতে হয় । টাইপস্ক্রিপ্ট (TypeScript) এতে এরর দেয় কারণ সে req.user চেনে না।

- কিভাবে কাজ করে (সম্ভাব্য কোড): সাধারণত একটি types.d.ts ফাইলে এভাবে লিখা হয়:

```ts
// src/types/express.d.ts
import { User } from "@prisma/client";

declare global {
  namespace Express {
    interface Request {
      user?: User;
    }
  }
}
```

- ব্যাখ্যা:
  এটি টাইপস্ক্রিপ্টকে বলে দেয় যে, "দেখো, এক্সপ্রেসের যে Request টাইপ আছে, তার ভেতরে user নামেও একটি ফিল্ড থাকতে পারে।"
  এর ফলে যখন কন্ট্রোলারের ভেতর req.user.id লিখা হবে, তখন টাইপস্ক্রিপ্ট আর কোনো এরর দেবে না এবং অটো-সাজেশন দেখাবে।

---
