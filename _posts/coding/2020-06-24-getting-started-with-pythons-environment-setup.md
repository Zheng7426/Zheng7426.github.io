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

You can find mean value in a matrix by the <code>np.mean()</code> method.

```
np.mean(x, axis=1)
np.mean(x, axis=0)
```
![Jupyter Notebook step 17](/images/python_env/jupyter_17.png)

Notice that in the context of NumPy, axis 1 is the axis that runs horizontally across the columns, while axis 0 is the axis that runs vertically along the rows.

![Jupyter Notebook step 18](/images/python_env/jupyter_18.png)

Did I mention that Dot Product is a very common tensor operation? Now it is an appropriate time to briefly introduce the concept of tensors. After all, we created our Tensorflow environment with Conda, and it is fairly likely that Tensorflow would be related to tensors.  

A tensor could be viewed as a container for numerical data(in most cases).  

A 0-dimensional tensor only contains one number, such as 2020, and 0D tensor is also called a scalar. We can use the <code>ndim</code> method to check the number of dimensions of a NumPy tensor.

![Jupyter Notebook step 19](/images/python_env/jupyter_19.png)

A 1D tensor contains an array of numbers, it is also called a vector.

![Jupyter Notebook step 20](/images/python_env/jupyter_20.png)

We have already dealt with 2D tensors, also known as matrices. A matrix contains an array of vectors.

![Jupyter Notebook step 21](/images/python_env/jupyter_21.png)

<br>
There are higher-dimensional tensors, but we are not going to dive that deep for now. Since we have had a glimpse of how to run Python on the local Jupyter Notebook environment, it is time to try coding on an online platform. Let us go to [Google’s Colab](https://colab.research.google.com/notebooks/intro.ipynb).

Colab is an abbreviation for Collaboratory. Google’s Colab helps you write and run Python code in your browser with zero configuration. That means you would not need to manually install packages as we did previously using Conda package manager. We can directly import needed packages and implement them on the fly.

When you click the above Google’s Colab link, you might be directed to a Colab’s homepage. The web page is built on an interactive environment called the Colab notebook. Colab notebooks are Jupyter Notebook hosted by Colab. Therefore, the way to write code on the Colab notebook is almost identical to how you wrote code on your local Jupyter Notebook. The Python codes would be executed on Google’s cloud servers. Thus, your local machine’s computation power becomes irrelevant. If you have a browser and internet connection, you are ready to go.

Let us create a new Colab notebook from the homepage.

![Google's Colab step 1](/images/python_env/colab_1.png)

Since we have touched upon tensors. Let us import TensorFlow and create a tensor, without explicitly dealing with the NumPy package. Note that we did not install TensorFlow, it would be fetched online for us. This also applies to other packages such as Pandas, Sci-kit Learn, Keras, and so on.

```
import tensorflow as tf
tf.constant(2020) 
```

Press the play button or <code>SHIFT</code>+<code>ENTER</code> to run the code cell.

![Google's Colab step 2](/images/python_env/colab_2.png)

As shown above, we use <code>tf.constant()</code> to create a tensor. We could also create a 2D tensor.

![Google's Colab step 3](/images/python_env/colab_3.png)

In order to create mutable tensors that have values we can modify, we could use <code>tf.Variable()</code>.

```
v = tf.Variable([[1., 2., 3.], [4., 5., 6.]])
v = tf.square(v)
v += 2020
```

You can apply different kinds of tensor operations.

![Google's Colab step 4](/images/python_env/colab_4.png)

Since Colab notebooks are stored on your Google Drive account, you can mount your Google Drive to gain access to your files from the Colab notebook environment.  

```
from google.colab import drive
drive.mount('/content/drive')
```

![Google's Colab step 5](/images/python_env/colab_5.png)

After you copy and paste the authorization code to access your Google Drive, press <code>Enter</code>.

![Google's Colab step 6](/images/python_env/colab_6.png)

Then you may use the Pandas package to read the CSV file stored on your Google Drive folders. Do not worry about how to use Pandas for now because we are still in the process of exploring different approaches to Python’s environment setup. One drawback of using Colab is that if your notebook has been idle for a certain period of time, the space on the cloud server would be released and you would have to run your cells again.

<br>
So far, we have explored how to run Python on Command Line Interface(Anaconda Prompt), Jupyter notebook through Anaconda Navigator, and also on Google’s Colab. Lastly, we are going to run Python on Pycharm. Pycharm is a Python IDE(Integrated Development Environment).

Let us head to [Pycharm’s download page](https://www.jetbrains.com/pycharm/download/) and select Community Edition.

![Pycharm step 1](/images/python_env/pycharm_1.png)

![Pycharm step 2](/images/python_env/pycharm_2.png)

![Pycharm step 3](/images/python_env/pycharm_3.png)

![Pycharm step 4](/images/python_env/pycharm_4.png)

![Pycharm step 5](/images/python_env/pycharm_5.png)

![Pycharm step 6](/images/python_env/pycharm_6.png)

After the installation process is completed, open the Pycharm desktop application. Click on Configure.

![Pycharm step 7](/images/python_env/pycharm_7.png)

In the configuration dropdown list, select Settings.

![Pycharm step 8](/images/python_env/pycharm_8.png)

Select Project Interpreter.

![Pycharm step 9](/images/python_env/pycharm_9.png)

In the Project Interpreter page, click the gear button and select Add.

![Pycharm step 10](/images/python_env/pycharm_10.png)

In the left-hand section, select Conda Environment. Then check the Existing environment radio button, as we have already created a Tensorflow environment called my_first_env. Click OK to exit this Interpreter Adding window.

![Pycharm step 11](/images/python_env/pycharm_11.png)

Select the interpreter we have just added. Click Apply, then click OK to finish this configuration process. Now select Create New Project.

![Pycharm step 12](/images/python_env/pycharm_12.png)

Now the Project Interpreter would be set to the one we just added. If you did not see this window, you might simply restart the computer and then launch PyCharm again. After that, you can specify the location of your new project, as shown below.

![Pycharm step 13](/images/python_env/pycharm_13.png)

![Pycharm step 14](/images/python_env/pycharm_14.png)

Click Create and then the initialization for your new project would begin.

To create a Python script, click the File tab on the top left corner and select ‘New…’

![Pycharm step 15](/images/python_env/pycharm_15.png)

Then select Python File.

![Pycharm step 16](/images/python_env/pycharm_16.png)

![Pycharm step 17](/images/python_env/pycharm_17.png)

Since we are using the Tensorflow environment as Project Interpreter. We have already installed packages like pandas, therefore, we could import them here. And in order to run the program, click the Run tab on the top toolbar.

![Pycharm step 18](/images/python_env/pycharm_18.png)

Select which Python file we want to execute.

![Pycharm step 19](/images/python_env/pycharm_19.png)

The output has been shown on the bottom window.

![Pycharm step 20](/images/python_env/pycharm_20.png)

This concludes our journey of Python environment setup. You may choose the most comfortable approach to write and execute your Python code. In general, writing in Jupyter Notebook is more flexible, because you execute one cell after another and the result of each cell would be displayed. On the other hand, if you are going to build a fairly complex application that requires a debugger, an IDE serves the purpose better.

References:

* _[Anaconda User Guide](https://docs.anaconda.com/anaconda/user-guide/)_

* _[NumPy Quick Start Tutorial](https://numpy.org/doc/stable/user/quickstart.html)_

* _[Colaborotary Intro](https://colab.research.google.com/notebooks/intro.ipynb)_

* _[PyCharm documentation](https://www.jetbrains.com/help/pycharm/quick-start-guide.html)_

* _Deep Learning with Python - Francois Chollet_



























