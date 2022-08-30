# f API

This API is a necessary step in the NSO account authorization process. There is an Android emulator on imink's server with the NSO client installed in it, and the f-parameters are generated by this client. It is completely free, you just need to tell me what project you use it in.

## Usage

You can use the f API already used in imink.

**URL:** `POST` `https://api.imink.app/f`

**Header:** You must send the correct `User-Agent` to let me know that you are requesting it. I suggest the format is: `{{ Your app name }}/{{ Your app version }}`.

**Body:** `JSON`

* token : `String`, **Required**. Get it from NSO api
* hash_method : `Number or String`, **Required**. 1 or 2
* timestamp : `Number or String`, Optional. It is not recommended to use this parameter
* request_id : `String`, Optional. It is not recommended to use this parameter

NOTE: timestamp and request_id will be generated by the server if not submitted. It is recommended to use the api generated timestamp and request_id. If you try to submit your own timestamp, it may cause the NSO api to return a 9599 error.

**Example:**

```
curl -X "POST" "https://api.imink.app/f" \
     -H 'User-Agent: {{ Your app name }}/{{ Your app version }}' \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
  "token": "{{ token }}"
  "hash_method": {{ 1 or 2 }},
}'
```

**Response:**
```
{
  "request_id": "c6e9d62d-7c05-4c9a-8f1a-b6d799fdd5ff",
  "timestamp": 1661355877196,
  "f": "543f7e9c4f3d3b5254a3772d211a8c093888b32991002c353f278bc8766face4b548f1bdaea24c9a58e5012b"
}
```

## Deploy your own f API

### Download

I modified the official version of NSO to make a new APK. It is easy to let you create your own f API. you can download the latest version from [Releases](https://github.com/imink-app/f-API/releases).

### How to use

1. Install the APK you downloaded into your Android system and it will show up as the NSO icon.
2. Launch it.

Now you can access it via `http://ip:9000`. ip needs to be replaced with the ip address of your Android device. The request parameters are exactly the same as `api.imink.app/f`.

Yes, it's that simple!

* You don't need to root your Android.
* You don't need to connect to a computer.

## How is this APK made

1. Cracking the signature verification of NSO.
2. Decompile apk to smali code.
3. Insert HTTP Server code and call libvoip.so to compute the f code in smali code.
4. Repackage as apk.
5. Re-sign.

The tools used are: jarsigner, Apktool, Xpatch, Android Studio.

Now here is just a simple description of the steps. More code and actions I will update in the future.
