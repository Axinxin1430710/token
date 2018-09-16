运用redis缓存生成的token值，并加上时效性，也就是缓存过期时间
        $accessToken = get_nonce_str();//生成随机字符串。访问控制令牌
        $refreshToken = get_nonce_str();//生成随机字符串。刷新控制令牌，用于令牌过去刷新
        $redis = new MyRedis();//获得redis缓存对象
        $user = [
            'token' => [
                'access_token' => $accessToken,
                'refresh_token' => $refreshToken,
                'expire_time' => time() + 7200,
                're_expire_time' => time() + 14400
            ]
        $redis->hSet($key, $field, json_encode($user));//设置缓存字段
        $redis->close();//关闭缓存对象




 sql 注入攻击 
 1、数字攻击
 查询条件 id=1 OR 1=1  =>  select *from table where id = 1 OR 1=1; 

 2、字符串攻击

 通过sql注释
 a、在查询条件下使用 # 注释后面的查询条件 例如查询语句 'select *from table where userName = james'#password = 1232';//把passsword查询条件注释
 b、查询条件下使用 -- 注释