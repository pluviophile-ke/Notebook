新建项目（待写）

​	DLL和通用DLL的区别

​	UWP DLL的版本选择



头文件

```c++
#pragma once

#define FUNCTION_EXTERN_API extern "C" __declspec(dllexport)

extern "C"
{
	typedef struct IMUInputForUnity
	{
		double x;
		double y;
		double z;
	}INPUT;

	typedef struct IMUOutputForUnity
	{
		double x;
		double y;
		double z;
	}OUTPUT;
}

namespace HL2Stream
{
	FUNCTION_EXTERN_API int __stdcall GetIMUStreaming(INPUT* input, OUTPUT* output);
}
```





源文件

```c++
#include "pch.h"
#include "LearnAcceleratePlugin.h"

namespace HL2Stream
{
	int __stdcall GetIMUStreaming(INPUT* input, OUTPUT* output)
	{
		output->x = input->x * input->x;
		output->y = input->y * input->y;
		output->z = input->z * input->z;

		return 200;
	}
}

```





生成设置





导入unity

​	plugins文件夹

​	WSAPlayer文件夹





更改平台





unity代码调用

```c#
[DllImport("LearnAcceleratePlugin", EntryPoint = "GetIMUStreaming", CallingConvention = CallingConvention.StdCall)]
static extern int GetIMUStreaming(ref INPUT pv1, ref OUTPUT pv2);
```





