### Question

### v-if和v-for哪个优先级高？
    一般不把v-for与v-if用在同一个元素上，如果用在同一个元素，在vue中v-for的优先级要比v-if高。
### 如果两个同时出现，应该怎么优化得到更好的性能？

#### （1） 如果同时出现v-if的作用是为了控制v-for是否执行，可以把v-if提出来

<font color=pink>bad</font>
``` 
    <ul>
        <li
            v-for="user in users"
            v-if="shouldShowUsers"
            :key="user.id">
            {{ user.name }}
        </li>
    </ul>
```
<font color=lightgreen>good</font>
```
<ul v-if="shouldShowUsers">
    <li
        v-for="user in users"
        :key="user.id" >
        {{ user.name }}
    </li>
</ul>
```

#### （2）如果是为了将列表中的一些项不显示，可以提前把列表过滤一下
<font color=pink>bad</font>
``` 
    <ul>
        <li
            v-for="user in users"
            v-if="user.isActive"
            :key="user.id">
            {{ user.name }}
        </li>
    </ul>
```
<font color=lightgreen>good</font>
```
computed: {
  activeUsers: function () {
    return this.users.filter(function (user) {
      return user.isActive
    })
  }
}
<ul>
  <li
    v-for="user in activeUsers"
    :key="user.id">
    {{ user.name }}
  </li>
</ul>

```
