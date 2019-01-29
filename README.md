# school_service_api
校园服务API 说明

## 请求七牛获取上传令牌 API##

> GET: localhost:8080/upload_token

返回值：K8WWlWVTd6-p4WzoIh0IygahkTXgy2dztQVD1Tpk:6Jqlv1acNfKDYI8r1WIzs1WNQDE=:eyJzY29wZSI6InNjaG9vbHdhbGwiLCJkZWFkbGluZSI6MTU0ODc0NDA4MH0=

## 获取用户信息和微信返回的openid API##

### 1 返回session_key 和 openid ###

> GET： localhost:8080/wxlogin/{code}

参数：code

返回值：{"session":"XXX","openid":"XXXXX"}

### 2 查询此用户是否授权 ###

> GET： localhost:8080/ishasUser/{openid}

参数：openid

返回值：{"result":true/false}

### 3 授权此用户 ###
>Post： localhost:8080/authorizeUser

参数:openid、nickname、avatarurl、province、city、gender

    {"openid"："CCC",
     "nickname":"XXXX",
    "avatarurl":"DDDD",
    "province":"sssss",
    "city":"DDD",
    "gender":1
    }

返回值：{"result":true/false}

### 4 查询用户信息 ###
> GET： localhost:8080/userinfo?openid=xxxx

参数： openid

返回值:

    {
	"id": 2,
	"openid": "oBjXq0JoFULN4P4wHXt_mYzI8AMg",
	"nickname": "漠然",
	"avatarurl": "https://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTLeSJU2zvIXrLF9TJfz0VUSic9kxJ8LHKuyeKHL6EeSS4afmjSUiaianvhf7sBt7531qElssKWlsx5MA/132",
	"province": "宁夏",
	"city": "银川",
	"gender": 1
	}

## 表白墙相关 API ##

### 1 分页查询表白墙信息 ###
> GET : localhost:8080/conf/confessionDataList?openid=XXX&page=X&pageSize=XX

参数：openid、page、pageSize

返回值：


    [{
	"id": "70e529fd-f92d-11e8-b496-525400f4c464",
	"content": "我常常想我是幸运的，在慌张彷徨的年华里，总能遇到一群志和道同的朋友， 我常常也想我一定是这世界上最不幸的，苍狗白云，白驹过隙间，我又总是与他们流离失散。 ​​​",
	"time": "2019/01/28",
	"likedCount": 2,
	"liked": 0,
	"stateNiming": 1,
	"user": {
		"avatar": "https://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTIZNXcA9x76UOORpEicUTUFCqZiat6mfh7e6R4jVaKJqZTYOicS0icUYQ9oxqYRibW4zKj5Qq0DibPowgUA/132",
		"touser": "222",
		"fromuser": "我叫胡颜德",
		"userId": "oBjXq0LC0fNVc74SoTZTYj7OSMKc",
		"sex": 1
	},
	"images": ["http://zwxq.qiqibl.com/tmp_5f9195e2ea66c50deb6cf9ed9f435f0b.jpg"]
	}, {
	"id": "ce31bc14-0f7e-11e9-b4a9-525400f4c464",
	"content": "虽然你拒绝了我 但我依旧等你 喜欢一个人 真的会中毒的",
	"time": "2019/01/28",
	"likedCount": 3,
	"liked": 1,
	"stateNiming": 1,
	"user": {
		"avatar": "https://wx.qlogo.cn/mmopen/vi_32/icjdyu7IemU9GTMdI9POUm7ic0mNqhACv15reuWruJpVaUeGdwb7oBziaRhTBKAUvia1t3GjSbyQYUUvlubVpEwLFQ/132",
		"touser": "18汉语言小姐姐",
		"fromuser": "ssss",
		"userId": "oBjXq0K--hdqNF3w0fpvfbNWHiY4",
		"sex": 0
	},
	"images": []
	}]

### 2 新增信息 暂定 ###


### 3 点赞处理 ###
> GET ：localhost:8080/conf/tapLike?confid=XX&openid=XXX&likedstate=XXX

参数：confid 、openid、likestate(点赞状态 0 1)

返回值：

    {"likedstate":false,"likecount":-1}
    {"likedstate":false,"likecount":1}


### 4 查看留言 ###
> GET： localhost:8080/conf/confMessages?confid=XX&page=XXX&pageSize=XXX

参数：confid、page、pageSize

返回值：

    {
	"data": [{
		"openid": "oBjXq0JoFULN4P4wHXt_mYzI8AMg",
		"avatarurl": "https://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTLeSJU2zvIXrLF9TJfz0VUSic9kxJ8LHKuyeKHL6EeSS4afmjSUiaianvhf7sBt7531qElssKWlsx5MA/132",
		"nickname": "漠然",
		"message": "fdfdsf",
		"cratetime": "01-29"
	}, {
		"openid": "oBjXq0JoFULN4P4wHXt_mYzI8AMg",
		"avatarurl": "https://wx.qlogo.cn/mmopen/vi_32/Q0j4TwGTfTLeSJU2zvIXrLF9TJfz0VUSic9kxJ8LHKuyeKHL6EeSS4afmjSUiaianvhf7sBt7531qElssKWlsx5MA/132",
		"nickname": "漠然",
		"message": "dffds",
		"cratetime": "01-29"
	}, {
		"openid": "oBjXq0CMC9JgKVd44tUjBgtOiMfE",
		"avatarurl": "https://wx.qlogo.cn/mmopen/vi_32/7fGlqgcudKkFrCiauWicFkKAib1UtHOQHxsDSxekIvCv6MVvMKhgYnicIjmS7oYmccDyV6cPibMGjK29DvSeeh10Oog/132",
		"nickname": "昵称",
		"message": "dsdsdsddd",
		"cratetime": "01-28"
	}],
	"other": 3, #数量
	"message": "confession message list"
	}

### 5 新增留言  ###