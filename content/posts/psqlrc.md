---
title: "psql and the .psqlrc configuration file"
date: 2018-09-02
tags: [PostgreSQL, psql, psqlrc]
---

If you use PostgreSQL, do yourself a favor and try [psql](https://www.postgresql.org/docs/current/static/app-psql.html). GUI tools rightly deserve a place in the ecosystem and many developers might find them easier to tackle, especially if they lack familiarity with PostgreSQL. I have myself used PgAdmin, DBeaver, OmniDB, ... If you've leveled up as a now power user, psql, with its scripting abilities, numerous options should be your tool of choice.

In this short article, I will concentrate on a very tiny part of psql, its configuration file, usually located in the home directory (~/.psqlrc). First of all, what are the pros and cons of having such a file ? On the positive side:

 - customize your psql experience;
 - define your own prompt;
 - output the query results the way you want: borders, NULL display, format, ...
 - define some variables, custom queries and reuse them with ease. For example, you could define a query to know the servers uptime, and simply use it with `:uptime`;
 - change your history settings;

On the negative side:

 - you should know the default settings as not every server will have your psql configured the way you want;
 - if you have some scripts that use psql, a .psqlrc file might break them. You might have to use `psql --no-psqlrc` instead;
 - with great power comes great responsability;

As a whole, it might be a useful tool to know, especially if you often connect to the same server(s). If you're into good looking output, here is one example of what can be changed:

```
postgres=# select current_user;
+--------------+
| current_user |
+--------------+
| postgres     |
+--------------+
(1 row)
```

By setting:

```
\set PROMPT1 '%n@%/ %# '
\pset border 2
\pset linestyle unicode
```

Will produce the following output:

```
postgres@postgres # select current_user;
┌──────────────┐
│ current_user │
├──────────────┤
│ postgres     │
└──────────────┘
(1 row)
```

By setting the so called "specially treated variables", you can change more interesting (and sometimes dangerous) settings such as AUTOCOMMIT, ENCODING, VERBOSITY, ...  There are dozens of them. As always, please refer to the [documentation](https://www.postgresql.org/docs/current/static/app-psql.html) and the [wiki](https://wiki.postgresql.org/wiki/Psqlrc) for all the gory details.

And if you wish to have a look at example .psqlrc files, I maintain one in [Github](https://github.com/e7e6/psqlrc). It is updated to work with PostgresSQL 10 and can be used as a template for your own needs.

