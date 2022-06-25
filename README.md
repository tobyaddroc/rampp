# rampp
Good library for coding cheats for games

# Usage:
1. Clone this repo
2. Put "rampp" to your project
3. Add #include "rampp" in your code

# API
> If you want use rampp methods in your own functions, mark them as __rampp (int __rampp main)
> The rampp methods are accessed via #define (rampp.Attach(..., ...))

> Attach(PID, WindowName) - bool
Attach allows you to connect to a process and get its global handle for further work, whether it's writing or reading from memory
Usage: while (!rampp.Attach("hl2.exe", "Counter-Strike Source")) { Sleep(1000) }

> Detach() - void
Detach closes all handles that were previously opened to work with memory
Usage: rampp.Detach();

> GetModuleBaseAddress(ModuleName) - DWORD (unsigned long)
Returns the address of the module that you specify with the method call parameters
Usage: DWORD dwAddress = rampp.GetModuleBaseAddress("client.dll");

> Protect() & Vulback() - void & void
Freezes all handles of the process you are attached to, most often used to protect against anti-cheat
Usage: rampp.Protect(); & rampp.Vulback();

> Read<type>(Address) & Write(Address, Value) - (returns the type you specified) & void
Allows reading and writing to process memory
Usage: DWORD dwValue = rampp.Read<DWORD>(dwAddress); & rampp.Write(dwAddress, NULL);

> FindPattern(ModuleName, Pattern, Offset_of_pattern, Offset_of_address, Subtract) - uintptr_t or DWORD (unsigned long)
Finds an address by signature in a specific module
Usage: DWORD NewdwAddress = rampp.FindPattern("client.dll", "9F ? 5F 9A ? ? 00", 0x0, 0x0, 1);

> PidByWindowName(HWND, WindowName) - DWORD (unsigned long)
Gets the process id from its window name + fills global pid (needs for attach, but not necessary)
Usage: DWORD pid = rampp.PidByWindowName(0, "Counter-Strike Source");

> GetPid() - DWORD (unsigned long)
Returning global pid
Usage: DWORD pid = rampp.GetPid();
  
> GetHandle() - HANDLE
Returning global handle
Usage: HANDLE handle = rampp.GetHandle();
