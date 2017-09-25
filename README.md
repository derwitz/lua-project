# lua-project
lua语言脚本
package.path  = '/home/www/bin_lua/?.lua;;./?.lua;' .. package.path

-- config example
<pre>
local config = {
    redis_a = {your connection name 
        host = '127.0.0.1',
        port = 6379,
        pass = '',
        timeout = 200, -- watch out this value
        database = 0,
    },
    redis_b = {
        host = '127.0.0.1',
        port = 6379,
        pass = '',
        timeout = 200,
        database = 0,
    },
}

local redis_factory = require('redis_factory')(config) -- import config when construct
local ok, redis_a = redis_factory:spawn('redis_a')
local ok, redis_b = redis_factory:spawn('redis_b')
local ok = redis_a:set('test', "aaaaaaaaaaa")
if not ok then ngx.say("failed") end
local ok = redis_b:set('test', "bbbbbbbbbbb")
if not ok then ngx.say("failed") end

redis_factory:destruct() -- important, better call this method on your main function return

ngx.say("end")
</pre>