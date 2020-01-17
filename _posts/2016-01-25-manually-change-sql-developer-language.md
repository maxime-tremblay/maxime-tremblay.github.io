---
layout: post
title: Manually Change SQL Developer Language
tags: [SQL Developer]
---

If like me your OS is not in English, but you would prefer to have SQL Developer be in English, after looking at all of the preferences options, you will find that there is no option to change SQL Developer's language.

It's still possible to do it manually though.

Here are the steps you need to follow:
- Close SQL Developer
- From the root of SQL Developer folder, go into the `sqldeveloper\bin` subfolder.
- Edit the `sqldeveloper.conf` file
- Append this at the end

``` texte
#Force English
AddVMOption -Duser.language=en
```

SQL Developer should now be in English.