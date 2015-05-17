# What is RPC handle(r) ? #
[Rbitter](https://github.com/nidev/rbitter) stores your tweets in database via ActiveRecord.

However, just saving is not enough. You may want to access archived tweets and review some tweets. So, Rbitter provides XMLRPC daemon. Using it, you can achieve your goal.

You can write your own RPC handler, too. Please see below sections.

## Basics

XMLRPC utilizes XML format to exchange data over RPC service. XML data will be decoded into native represented data type like String, Array, Hash and so on.

In other words, data in ActiveRecord of Rbitter can be transformed into any type supported by XMLRPC protocol and client which has requested before will get language-native-type data. The ways are different from each whomever will code XMLRPC handle.

Handlers here will be use stringified format. Though it is not documented, still it is good enough for testing purpose.

## Commands ##
### Authentication ###
### Revoke Authentication Token ###
### Echo ###
### Last Active ###
### Retriever ###
### Statistic ###
# How to write own RPC handle? #
RPC handle is a Ruby class. Writing a method in Ruby class, that's it. Names of methods are treated as XMLRPC command.

When you write a new class for your own RPC handle, you must inherit either Auth or NoAuth class from rpc/base.rb.

* class Auth < Object: Methods in a Ruby class inheriting Auth requires *auth_key* to access.
* class NoAuth < Object: Methods in a Ruby class inheriting NoAuth doesn't require *auth_key* and these XMLRPC commands can be called by anonymous user.

Filename should start with 'rh_'. It's prefix to be autoloaded by xmlrpc.rb.

Refer rh_echo.rb as an example.
