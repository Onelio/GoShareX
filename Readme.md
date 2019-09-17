# GOSHAREX
A simple Custom ShareX Uploader using only standard built-in Go packages. 

PD: Although this tool can be compiled for Windows and Linux the client software(ShareX) is only available for Windows.

### Version 2
- Filenames are generated from unixnano base64 encoded
### Version 1
- Filenames are generated from file MD5 Sum

# Installation
````
go get github.com/Onelio/GoShareX

./GoShareX
---- or ----
GoShareX.exe
````

# Options:
- `domain` Set Domain/IP:Port to listen (Default ":80")
- `output` Set output system directory for storage - will be created if not exist (Default "out")
- `path` Set virtual path for previewing files (Default "/!/")
- `secret` Shared secret between ShareX and server for auth - allow everything if none (Default "")
- `iplist` Coma separated list of every dir-listing allowed address (Default "127.0.0.1")
- `size` Max Upload size in MB (Default 10)

# ShareX Configuration
Setting ShareX custom uploader can be done with a `.sxcu` file like __config_example.sxcu__. You just need to change the domain and secret to fit yours.

````
{
   "Version":"13.0.1",
   "DestinationType": "ImageUploader, TextUploader, FileUploader",
   "RequestMethod":"POST",
   "RequestURL":"http:{YOUR_DOMAIN}/upload",
   "Body":"MultipartFormData",
   "FileFormName":"file",
   "Arguments":{
      "secret":"{YOUR_SECRET}",
   }
}
````

Remember that uploads will allways be made to __/upload__ with a POST method and a valid secret and file. Anything else will return 404.

# FAQ

**Q:** *Can't upload anything with secret ""*

**R:** Remove secret from the CustomUploader settings as argument.

**Q:** *Upload fails with "http: no such file"*

**R:** Check that your "FileFormName" value is "file" and that you are uploading images, files or text only.

**Q:** *Upload returns 404 with valid secret*

**R:** Check that your file does not exceeds the max allowed (10MB by default).

**Q:** *Can't preview the dir-listing on localhost*

**R:** Localhost works different from remote. This is a known bug.
