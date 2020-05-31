---
layout: post
title:  "PPM Files"
date:   2020-05-30 12:00:00 +0900
categories: file format, ppm
---
PPM is a very simple image format. It stands for “Portable PixMap”. Actually, it is from a family of portable image formats. What’s nice about them is that they are very simple. They are text based, and have a very simple structure, just a small header area followed by uncompressed data. You can find more information about them here.

That’s all well and good, but how do we create them? Here is a simple function for creating a PPM image and saving random colour data to it.

{% highlight c++ %}
void savePPM(const char* Filepath,const int Width,const int Height)
{
    std::ofstream fout(Filepath);
    if(fout.fail()) {
        std::cout << "Cannot save image\n";
        return;
    }
    fout << "P3\n"; // PPM header tag
    fout << Width << " " << Height << '\n'; // resolution
    fout << "255\n"; // highest value
    for(int y=0; y<Height; ++y)
    {
        for(int x=0; x<Width; ++x)
        {
            fout << int(rand()%256) << " ";
            fout << int(rand()%256) << " ";
            fout << int(rand()%256) << "   ";
        }
        fout << '\n';
    }
    fout.close();
}
{% endhighlight %}

You can see how to save pixel data you generate. Most operating systems and image viewing software will know how to read and write PPM files, so that are a very easy way to programatically create image files. 

![Writing random pixels](/assets/images/random.png)

Now that we have the ability to write pixels and display them, we can get started generating arrays of pixels to save. What shall we do first? Raytracing? Cellular Automata? Reaction Diffusion systems? Fractals? Fluid Simulations? The choices are endless.
