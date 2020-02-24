# Create and use one Dynamic Link Library (C++)

**Original Source:**  
https://docs.microsoft.com/en-us/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp?view=vs-2019  

**Introduction:**  
This code shows a sample of using the Visual Studio IDE to create a dynamic link library (DLL) written in Microsoft C++ (MSVC), and then using the DLL from another C++ app. In this code, a DLL is created that implements some math functions. Then a console app that uses the functions from the DLL is created.  

**This code covers these tasks:**
1. Create a DLL project in Visual Studio.
2. Add exported functions and variables to the DLL.
3. Create a console app project in Visual Studio.
4. Use the functions and variables imported from the DLL in the console app.
5. Run the completed app.  

**Platform:** Windows 10 x64.  
**IDE:** Visual Studio 2017.  
**Configuration:** Debug mode.  

**Create a client app that uses the DLL**  
When you create a DLL, think about how client apps may use it. To call the functions or access the data exported by a DLL, client source code must have the declarations available at compile time. At link time, the linker requires information to resolve the function calls or data accesses. A DLL supplies this information in an import library, a file that contains information about how to find the functions and data, instead of the actual code. And at run time, the DLL must be available to the client, in a location that the operating system can find.

Whether it's your own or from a third-party, your client app project needs several pieces of information to use a DLL. It needs to find the headers that declare the DLL exports, the import libraries for the linker, and the DLL itself. One solution is to copy all of these files into your client project. For third-party DLLs that are unlikely to change while your client is in development, this method may be the best way to use them. However, when you also build the DLL, it's better to avoid duplication. If you make a local copy of DLL files that are under development, you may accidentally change a header file in one copy but not the other, or use an out-of-date library.

*To avoid out-of-sync code, we recommend you set the include path in your client project to include the DLL header files directly from your DLL project. Also, set the library path in your client project to include the DLL import libraries from the DLL project. And finally, copy the built DLL from the DLL project into your client build output directory. This step allows your client app to use the same DLL code you build.*  

**To add the DLL header to your include path**
1. Right-click on the **MathClient** node in **Solution Explorer** to open the **Property** Pages dialog.  
2. In the **Configuration** drop-down box, select **All Configurations** if it's not already selected.  
3. In the left pane, select **Configuration Properties > C/C++ > General**.  
4. In the property pane, select the drop-down control next to the **Additional Include Directories** edit box, and then choose **Edit**.
