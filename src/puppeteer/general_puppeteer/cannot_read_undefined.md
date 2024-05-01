# [Cannot read properties of undefined (reading ‘\_id’)](https://forum.codewithmosh.com/t/cannot-read-properties-of-undefined-reading-id/18554)

[Node](https://forum.codewithmosh.com/c/node/9)

You have selected **0** posts.

[select all](https://forum.codewithmosh.com/t/cannot-read-properties-of-undefined-reading-id/18554)

[cancel selecting](https://forum.codewithmosh.com/t/cannot-read-properties-of-undefined-reading-id/18554)

Back

#### 1

/

#### 6

[![](https://avatars.discourse-cdn.com/v4/letter/j/278dde/48.png)](https://forum.codewithmosh.com/u/jtremochajr)

[jtremochajr](https://forum.codewithmosh.com/u/jtremochajr)

[Mar 2023](https://forum.codewithmosh.com/t/cannot-read-properties-of-undefined-reading-id/18554 'Post date')

Hi Mosh,

Got an error while getting the current user using GET method in postman. Here’s the error

NodeJs/vidly/routes/users.js:10

```typescript
const user = await User.findById(req.user.\_id).select(‘-password’);
^
TypeError: Cannot read properties of undefined (reading ‘\_id’)

const mongoose = require(‘mongoose’);
const express = require(‘express’);
const router = express.Router();
const \_ = require(‘lodash’);
const bcrypt = require(‘bcrypt’);
const auth = require(‘…/middleware/auth’);
const { User, validate } = require(‘…/models/user’);

router.get(‘/me’, auth, async (req, res) => {
const user = await User.findById(req.user.\_id).select(‘-password’);
res.send(user);
});
```
