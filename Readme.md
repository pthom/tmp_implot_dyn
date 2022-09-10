Sample repository to help work on implot PR https://github.com/epezent/implot/pull/397

This is a standard setup of imgui + implot sample, using GLFW + OpenGL3.

The file sample_implot_imgui.cpp is a simple copy of the imgui glfw+OpenGL3 sample, with this code added:

````cpp
struct MyPlotHandler
{
    MyPlotHandler() { mContext = ImPlot::CreateContext(); }
    ~MyPlotHandler() { ImPlot::DestroyContext(mContext); }
    void Draw()
    {
        static long values[] = {1, 3, 5, 7};
        ImPlot::BeginPlot("a");
        ImPlot::PlotLine("s", values, 4);
        ImPlot::EndPlot();
    }
    ImPlotContext* mContext;
};
````

And later in the render code:

````cpp

int main(int, char**)
{
        // init
        MyPlotHandler myPlotHandler;
    
        ...

        // inside the render loop
        myPlotHandler.Draw();

````

The link fails with the error "undefined reference to `void ImPlot::PlotLine<long>(char const*, long const*, int, double, double, int, int, int)`".

See for example
https://github.com/pthom/tmp_implot_dyn/runs/8284252337?check_suite_focus=true

````
[100%] Linking CXX executable sample_implot_imgui
/usr/bin/ld: CMakeFiles/sample_implot_imgui.dir/sample_implot_imgui.cpp.o: in function `MyPlotHandler::Draw()':
sample_implot_imgui.cpp:(.text._ZN13MyPlotHandler4DrawEv[_ZN13MyPlotHandler4DrawEv]+0x84): undefined reference to `void ImPlot::PlotLine<long>(char const*, long const*, int, double, double, int, int, int)'
collect2: error: ld returned 1 exit status
make[2]: *** [CMakeFiles/sample_implot_imgui.dir/build.make:101: sample_implot_imgui] Error 1
make[1]: *** [CMakeFiles/Makefile2:176: CMakeFiles/sample_implot_imgui.dir/all] Error 2
make: *** [Makefile:136: all] Error 2
Error: Process completed with exit code 2.
````