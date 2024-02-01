# c-c-
Cоздание dll


sudo apt install mingw-w64

x86_64-w64-mingw32-gcc-win32 shell.c -shared -lws2_32 -o VerifyThemeVersion.dll

python3 -m pefile exports VerifyThemeVersion.dll 
