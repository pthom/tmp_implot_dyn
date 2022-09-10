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

