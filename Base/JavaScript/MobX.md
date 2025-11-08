2025-05-31 19:31
Tags: #mobX

`npm i mobx`
`npm i mobx-react-lite` - связь mobX и React
`npm i mobx-utils` - утилиты

---

```ts
import { makeAutoObservable } from "mobx";

class CounterStore {  
  count: number = 0;  
  
  constructor() {  
    makeAutoObservable(this);  // настройки стора
  }  
  
  increment = (value: number) => {  
    this.count += value;  
  };  
  
  decrement = (value: number) => {  
    this.count -= value;  
  };  
}  
  
export default new CounterStore();
```

```tsx
import counterStore from "@/mobX/stores/counter-store.ts";  
import { observer } from "mobx-react-lite";  
  
export const Counter = observer(() => {  
  const { count, increment, decrement } = counterStore;  
  
  return (  
    <div className="flex justify-center items-center gap-4">  
      <button  
        className="w-8 bg-amber-500 cursor-pointer px-2 rounded-xl"  
        onClick={() => decrement(1)}  
      >  
        -  
      </button>  
      <span>{count}</span>  
      <button 
	    className="w-8 bg-amber-500 cursor-pointer px-2 rounded-xl"  
        onClick={() => increment(1)}  
      >  
        +  
      </button>  
    </div>  
  );  
});
```

---

Использование асинхронных операций
```ts
import { makeAutoObservable, runInAction } from "mobx";  
import apiService, { Post } from "@/mobX/services/api.service.ts";  
  
class PostsStore {  
  posts: Post[] = [];  
  isLoading: boolean = false;  
  
  constructor() {  
    makeAutoObservable(this);  
  }  
  
  getPosts = async () => {  
    try {  
      this.isLoading = true;  
      const res = await apiService.getPosts();  
  
      runInAction(() => {  
        this.posts = res.data;  
        this.isLoading = false;  
      });  
    } catch {  
      this.isLoading = false;  
    }  
  };  
}  
  
export default new PostsStore();
```

```tsx
import { observer } from "mobx-react-lite";  
import postsStore from "@/mobX/stores/posts-store.ts";  
  
export const Posts = observer(() => {  
  const { posts, isLoading, getPosts } = postsStore;  
  
  const getPostsHandle = () => {  
    getPosts();  
  };  
  
  return (  
    <div className="flex flex-col justify-center items-center gap-5">  
      {isLoading && "...loading"}  
      <button  
        className="bg-amber-500 cursor-pointer px-2 rounded-xl"  
        onClick={getPostsHandle}  
      >  
        get posts  
      </button>  
  
      <div>        {posts &&  
          posts  
            .slice(0, 10)  
            .map((post) => <div key={post.id}>{post.title}</div>)}  
      </div>  
    </div>  
  );  
});
```

---

Использоваине `mobx-utils`
```ts
import { makeAutoObservable } from "mobx";  
import apiService, { User } from "@/mobX/services/api.service.ts";  
import { IPromiseBasedObservable, fromPromise } from "mobx-utils";  
  
class UsersStore {  
  users: IPromiseBasedObservable<User[]> | null = null;  
  
  constructor() {  
    makeAutoObservable(this);  
  }  
  
  getUsers = () => {  
    this.users = fromPromise(apiService.getUsers().then((res) => res.data));  
  };  
}  
  
export default new UsersStore();
```

```tsx
import usersStore from "@/mobX/stores/users-store.ts";  
import { observer } from "mobx-react-lite";  
import { PENDING, REJECTED } from "mobx-utils/lib/from-promise";  
  
export const Users = observer(() => {  
  const { users, getUsers } = usersStore;  
  
  const getUsersHandle = () => {  
    getUsers();  
  };  
  
  if (users?.state === PENDING) {  
    return <div>...loading</div>;  
  }  
  
  if (users?.state === REJECTED) {  
    return <div>Error</div>;  
  }  
  
  return (  
    <div className="flex flex-col justify-center items-center gap-5">  
      <button  
        className="bg-amber-500 cursor-pointer px-2 rounded-xl"  
        onClick={getUsersHandle}  
      >  
        get users  
      </button>  
  
      <div>        {users?.value.length &&  
          users.value.map((post) => <div key={post.id}>{post.name}</div>)}  
      </div>  
    </div>  
  );  
});
```

---
### Links
