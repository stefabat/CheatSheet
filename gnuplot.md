### In the console

To plot data points store in 'datafile', the data should be organized in columns. The first row can include words labeling the content of the columns, and these can be automatically set to be in the legend. Separation between columns is arbitrary.

#### General comments

At any moment, if you need help just type `help` and choose the topic, and the subtopic if needed. Pressing Enter without typing anything will exit from the help pages. Every setting that can be `set` can also be `unset`. **All commands can be abbreviated by the first unique letters**, if there is ambiguity, gnuplot will complain.
Typing `quit` will exit from the gnuplot shell. Typing `reset` will `unset` **all** settings to their default values. Typing `save 'filename'` will save everything to disk, and `load 'filename'` will restore everything back. Typing `history` will show you the history of all your typed in commands. Typing `test` will show an overview of the line styles and line types set. Typing `show <setting>` will print the value assigned to that particular `<setting>`.
Note that all commands given below which specify an axis, such as `xrange` or `xlabel` are also valid for the y and z axis (when applicable) and are thus not written explicitly.

#### Set the terminal

    set terminal                    # shows the available terminals
    set terminal qt <n>             # plot to the qt gui number <n>, different numbers -> different windows!
    set terminal dumb               # plot to the terminal!
    set terminal pdf                # print to pdf (cairo)
    set terminal eps                # print to eps (cairo)
    set terminal postscript         # print to postscript (no cairo)
    set terminal cairolatex eps     # print to eps the figure and create a tex file for the text
    set terminal cairolatex pdf     # print to pdf the figure and create a tex file for the text

#### Output stream

    set output                      # set the default output / close a file if there is one open
    set output 'outfile'            # open file 'outfile' and write the output in it

After we have opened a file with `set output 'outfile'` and written in it, it is important **to close it** again with `set output`, otherwise the file will just remain empty. Note that when using `cairolatex`, we need to specify the latex file with `set output 'file.tex'`, and cairolatex will automatically create `file.pdf` with the figure.

#### Functions

    f(x) = x^2                                  # define a function called f(x)
    g(x,y) = 2.0*sin(x)+exp(y)                  # more than one variable, there are predefined functions too!
    h(x) = a*4.0 + b*sin(pi*x)                  # functions can have variables not yet set (i.e. a in this case)

#### Plot

    plot 'datafile' using 1:2                   # plot the first column in datafile as x and the second as y
    plot 'datafile' u 1:3 title columnhead      # plot the 1st and the 3rd column and use the text in the first row in the legend
    plot f(x)                                   # plot the function f(x)
    splot g(x,y)                                # plot the g(x,y) with lines
    splot g(x,y) with pm3d                      # plot the g(x,y) as a surface
    plot [xmin:xmax] [ymin:ymax] 'datafile'     # plot within a certain range
    replot f(x)                                 # superimpose the plot of f(x) to the previous plot
    plot 'datafile' u 1:2, '' u 1:3             # plot simultaneously two sets of data points
    plot 'datafile' with linespoints            # plot data points with points and lines
    plot 'datafile' with lp ls 2                # plot data points with points and lines of style number 2 (ls = linestyle)
    plot 'datafile' with lp lt 2                # plot data points with points and lines of type number 2 (lt = linetype)
    plot 'datafile' with lines lw 3             # plot data points with lines of width 3
    plot 'datafile' with l lc rgb '#e69f00'     # plot data points with lines of color #e69f00
    plot 'datafile' with points ps 4            # plot data points with points of size 4
    plot 'datafile' with p pt 7                 # plot data points with points of type 7
    plot 'datafile' with p lc rgb 'blue'        # plot data points with points of blue color

#### Fitting

    fit h(x) 'datafile' u 1:5 via a,b           # fit h(x) to the points in 'datafile', finding the best values for a and b -> assigns the values to a and b

#### Axes, grids, ranges, labels, tics, ...

    set grid                                    # set a grid in the background of the plot
    set xzeroaxis                               # set a dotted line as the x-axis
    set xzeroaxis linetype -1                   # adding linetype -1 makes it the same as the border lines
    set xrange [xmin:xmax]                      # set x range from xmin to xmax
    set xlabel 'Can contain \Latex code'        # set the axis label (Latex available using cairolatex term)
    set xtics xmin,dx,xmax                      # set tics from xmin to xmax every dx
    set xtics add (8,12,14,20)                  # set tics at those specific positions

#### Title, legend

    set title 'The title of the figure'         # set the title
    set key off                                 # turn legend off (on by default)

#### Set global styles

    help set style                              # to see all possible things that can be set
