---
title: "Using Conditionals in Pug"
date: 2022-09-29T22:54:16+05:30
draft: false
---

Pug provides if and unless conditionals

### if

```JS
- var userExist = true
  if userExist
    p.message welcome 
```

Output :-
```HTML
<p class="message">welcome </p>
```

```JS
- var userExist = true
  if userExist
    p.message welcome 
  else 
    p.message Invalid user
```

Output :-
```HTML
<p class="message">welcome </p>
```

### unless

*unless* works like a negated if. For instance, example using unless and if given below are equivalent.

#### Using unless
```JS
- var age = 19
  unless age < 18
    p.notification Eligible for vote
```

Output :-
```HTML
<p class="notification">Eligible for vote</p>
```

#### Using if
```JS
- var age = 19
  if age >= 18
    p.notification Eligible for vote
```

Output :-
```HTML
<p class="notification">Eligible for vote</p>
```
