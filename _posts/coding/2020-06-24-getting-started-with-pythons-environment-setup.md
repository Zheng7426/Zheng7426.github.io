---
layout: post
title: "Getting started with Python's environment setup"
date: 2020-06-24 00:00:00 -0000
categories: coding 
---

In the context of Machine Learning, there might be four ways to run Python on your computer:

* Command Line Interface(Terminal, Anaconda Prompt)
  
* GUI Software(Anaconda Navigator => Jupyter Notebook)
  
* Online platforms(Google's Colab, Deep Learning Virtual Machine on GCP)  

* IDE(Pycharm, Spyder)

In this article, we would go through all of the above approaches, so that you may find an approach that suits you best.

Let us start by downloading [Anaconda distribution](https://www.anaconda.com/products/individual). We would be using its Individual Edition. It contains four parts:

* Python - Source code of this programming language

* Conda - A package and environment manager

* Pre-installed scientific packages such as NumPy, Pandas, Sci-kit Learn

* Anaconda Navigator - A desktop Graphical User Interface to run applications, install packages without using Command-Line Interface.

Click on the 'Download' button, this would direct you to the Anaconda Installer section. You may choose various installers that fits your computer's system. We would download installers under Python 3.7.  
  
![anaconda installer](/images/python_env/download_anaconda_installer.gif)  

The installation procedure for both Windows and macOS is similar. Here we would illustrate how it is done in Windows.

![anaconda installer - windows](/images/python_env/installer_windows.png) 

After the installer is downloaded into your system, launch it.

![anaconda installer - windows step 1](/images/python_env/installer_windows_1.png) 

Continue to agree to the license agreement.

![anaconda installer - windows step 2](/images/python_env/installer_windows_2.png) 

![anaconda installer - windows step 3](/images/python_env/installer_windows_3.png) 

![anaconda installer - windows step 4](/images/python_env/installer_windows_4.png) 

![anaconda installer - windows step 5](/images/python_env/installer_windows_5.png) 

![anaconda installer - windows step 6](/images/python_env/installer_windows_6.png) 

![anaconda installer - windows step 7](/images/python_env/installer_windows_7.png)   
  
![anaconda installer - windows step 8](/images/python_env/installer_windows_8.png) 

After the installation finishes, search for and open ‘Anaconda Prompt’ from the start menu.

![anaconda prompt menu](/images/python_env/anaconda_prompt.png) 

As introduced earlier in the article, Conda is a package manager and environment manager. You can think of a Conda environment as a folder that contains certain packages that you have installed. For example, you may create one environment with Tensorflow installed and another one with Keras installed. If you change some dependencies on the environment with Tensorflow installed, the other environment which has Keras would not be affected. You can switch between different environments by activating and deactivating them.

We would go through how to create and activate a Conda environment now. And after that, we would install Tensorflow. Tensorflow is a powerful Python-friendly library for numerical computation, especially fine-tuned for Machine Learning.

It is documented that TensorFlow with Conda is supported on 64-bit Windows 7 or later, 64-bit Ubuntu Linux 14.04 or later, 64-bit CentOS Linux 6 or later, and macOS 10.10 or later.

Let us get started. Firstly, verify Conda has been installed by typing:

`conda --version`

![anaconda prompt step 1](/images/python_env/anaconda_prompt_1.png)

Let us name our Tensorflow environment as ‘my_first_env’.

`conda create --name my_first_env tensorflow`

![anaconda prompt step 2](/images/python_env/anaconda_prompt_2.png)

Hit <code>Enter</code> to run the previous command. If prompted Proceed<code>([y]/n)?</code> Enter <code>y</code>.

![anaconda prompt step 3](/images/python_env/anaconda_prompt_3.png)

Initially, you are running on the base environment. When the new environment has been created, switch to it by typing:

`conda activate my_first_env`

![anaconda prompt step 4](/images/python_env/anaconda_prompt_4.png)

Verify the new environment has been successfully activated by checking the current information of your environments:

`conda info --envs`

![anaconda prompt step 5](/images/python_env/anaconda_prompt_5.png)

Check your active environment’s Python version: 

`python --version`

![anaconda prompt step 6](/images/python_env/anaconda_prompt_6.png)

Since we are not in the base environment anymore, we would not have access to packages such as Pandas and Matplotlib. Thus, let us install a few useful packages into this new environment.

```
conda install -c anaconda pandas
conda install -c conda-forge matplotlib
conda install -c anaconda scikit-learn
conda install -c conda-forge keras
```

The installation command for each package might differ, as shown above. Do not be intimidated by those inconsistent installation commands. If you need to install a new package using Conda, you can search the package name on [Anaconda Cloud](https://anaconda.org/).

Hold on for a second, what are these packages for? We would get into details about how to use these packages in the future, and a brief introduction would suffice for now.

Pandas package offers a data structure for you to manipulate numerical tables. You can load your CSV(comma-separated-values) file into pandas’ DataFrame. And then you may query them just like you are dealing with databases.  

Matplotlib helps you with the visualization of data, and by using it you may generate various kinds of plots.  

Sci-kit Learn package provides you with various regression, classification, and clustering algorithms.  

There is another important package that we did not explicitly install, called Numpy. It has already been installed when we install Tensorflow with Conda. Numpy allows you to do mathematical operations with Python.  

To verify that Numpy has already been installed, let us write a small Python program in the Anaconda Prompt(Terminal on macOS).  

Firstly, type <code>python</code> and hit <code>Enter</code>:

![anaconda prompt step 7](/images/python_env/anaconda_prompt_7.png)

The <code>>>></code> sign means you are already running Python.

Type and run <code>print('Hello, I am in a new environment!')</code>

![anaconda prompt step 8](/images/python_env/anaconda_prompt_8.png)

Now let us import Numpy and give it an abbreviation as ‘np’.

```
>>> import numpy as np
>>> x = np.array([1, 2, 3, 4, 5, 6])
>>> print(x)
```
![anaconda prompt step 9](/images/python_env/anaconda_prompt_9.png)

Here we created a one-dimensional array and assigned it to a variable x. If no errors have been prompted to you, then we have verified that Numpy has already been installed, although we did not use <code>conda install</code> command to explicitly do it.

Let us exit this Python program for now. Simply type <code>exit()</code> and then press Enter.

![anaconda prompt step 10](/images/python_env/anaconda_prompt_10.png)

So far, we have run Python using Anaconda Prompt. We can also launch a Jupyter notebook using Anaconda Navigator to run Python. As mentioned before, Anaconda Navigator is a Graphical User Interface that does not involve Command Line Interface.

Click the Anaconda Navigator desktop application from the start menu.

![Jupyter Notebook step 1](/images/python_env/jupyter_1.png)

In Anaconda Navigator’s home page, we can various applications available. Let us first click on the Environments tab.

![Jupyter Notebook step 2](/images/python_env/jupyter_2.png)

![Jupyter Notebook step 3](/images/python_env/jupyter_3.png)

The environment we created a few minutes ago is shown here. If the activated environment is still the base(root), you can click on ‘my_first_env’ to activate this environment.

![Jupyter Notebook step 4](/images/python_env/jupyter_4.png)

After that, if you click on Open Terminal, you would see the familiar Anaconda Prompt that we interacted with a few minutes ago. Thus, Anaconda Navigator provides you with a user-friendly visual interface. you do not have to type in any commands, you can simply click on different buttons to achieve the same functionality.

Now let us click on the Home button and then press the ‘install’ button under Jupyter Notebook.

![Jupyter Notebook step 5](/images/python_env/jupyter_5.png)

Since we are not in the base environment, we shall install it first. After the installation, click on Launch to fire up a Jupyter server.

![Jupyter Notebook step 6](/images/python_env/jupyter_6.png)

If a web page does not appear, you can open up your browser and type in this address: <code>localhost:8888</code>. The Jupyter server would be listening to port 8888 by default.

![Jupyter Notebook step 7](/images/python_env/jupyter_7.png)

Now you can navigate to your desired directory, wherever you want to store Python scripts, models, or datasets.

You may create a new Python notebook by clicking the New button.

![Jupyter Notebook step 8](/images/python_env/jupyter_8.png)

Jupyter can handle multiple versions of Python, here we would select Python 3, the version we installed along with Anaconda.

![Jupyter Notebook step 9](/images/python_env/jupyter_9.png)

In general, a notebook has two types of cells: Code cell and text cell. For an empty notebook, initially, it only contains an empty code cell. We can type <code>print('Hello, world')</code> and click the play button(or press <code>Shift</code> + <code>Enter</code>) to execute this cell.

![Jupyter Notebook step 10](/images/python_env/jupyter_10.png)

The output is displayed below the first cell, and a new cell is automatically created because we have reached the end of the notebook.

If you need to write some plain text, simply change the cell type to Markdown.

![Jupyter Notebook step 11](/images/python_env/jupyter_11.png)

![Jupyter Notebook step 12](/images/python_env/jupyter_12.png)

Click on the play button again to run this text cell.

![Jupyter Notebook step 13](/images/python_env/jupyter_13.png)

Let us explore more about Numpy by creating multi-dimensional arrays.

```
import numpy as np
x = np.array([[1, 2, 3],
              [4, 5, 6]])
y = np.array([[7, 8], 
              [9, 10],
              [11, 12]])
```

We can print the shape of two matrices x and y.

![Jupyter Notebook step 14](/images/python_env/jupyter_14.png)

Dot Product is a very useful tensor operation. You can take the dot product of x and y only if the number of columns in x is equal to the number of rows in y.

![Jupyter Notebook step 15](/images/python_env/jupyter_15.png)

Let us get the dot product result.

`dot_product_result = np.dot(x, y)`

![Jupyter Notebook step 16](/images/python_env/jupyter_16.png)

Apart from <code>.dot()</code> method, there are various methods you could use. You can check its official documentation [here](https://numpy.org/doc/stable/user/quickstart.html).


















