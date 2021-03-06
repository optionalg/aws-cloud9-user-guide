.. Copyright 2010-2018 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0
   International License (the "License"). You may not use this file except in compliance with the
   License. A copy of the License is located at http://creativecommons.org/licenses/by-nc-sa/4.0/.

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
   either express or implied. See the License for the specific language governing permissions and
   limitations under the License.

.. _tutorial:

######################
Tutorial for |AC9long|
######################

.. meta::
    :description:
        Provides a hands-on tutorial that you can use to begin experimenting with AWS Cloud9.

In this tutorial, you set up an |envfirst| and then tour the |AC9IDElong|. Along the way, you use the IDE to code, run, and debug your first app.

This tutorial assumes you have already signed in to |AC9|. For more information, see one of the following:
   
* :ref:`setup-express-sign-in-ide` in :title:`Express Setup`.
* :ref:`setup-sign-in-ide` in :title:`Team Setup`.

.. note:: Completing this tutorial might result in charges to your AWS account. These include possible charges for |EC2|. For more information, see
   `Amazon EC2 Pricing <https://aws.amazon.com/ec2/pricing/>`_.

* :ref:`tutorial-create-environment`
* :ref:`tutorial-tour-ide`
* :ref:`tutorial-clean-up`
* :ref:`tutorial-next-steps`

.. _tutorial-create-environment:

Step 1: Create an |envtitle|
============================

An :dfn:`environment` is a place where you store your project's files and where you run the tools to develop your apps. In this section, you create an |envfirstec2|. An
:dfn:`EC2 environment` is an |env| that |AC9| connects to a newly-launched |EC2| instance running Amazon Linux.

.. note:: When you create an |envec2|, the |env| doesn't contain any sample code by default. To create an |env| along with sample code, skip this step, and see one of the following 
   topics instead: 
   
   * To create an |env| and connect it to an |EC2| instance preconfigured with a popular app or framework such as WordPress, MySQL, PHP, Node.js, Nginx, Drupal, or Joomla, or a Linux distribution such as 
     Ubuntu, Debian, FreeBSD, or openSUSE, you can use |lightsaillong| along with |AC9|. To do this, see :ref:`Working with Amazon Lightsail Instances <lightsail-instances>`. 
   * To create a more complex solution that includes a toolchain with the |AC9IDE|, source control, build, deployment, virtual servers or serverless resources, and more, 
     you can use |ACSlong| along with |AC9|. To do this, see :ref:`Working with AWS CodeStar Projects <codestar-projects>`.

   If you use |lightsail| or |ACSlong| to create your |env| and instance, we encourage you to come back to this topic, and then skip ahead to :ref:`tutorial-tour-ide` to learn how to use the |AC9IDE| to work 
   with your new code. 

To create a blank |envec2|, do the following:

#. After you sign in to the |AC9| console, in the top navigation bar, choose an AWS Region to create the |env| in. For a list of available AWS Regions, see 
   :aws-gen-ref:`AWS Cloud9 <rande.html#cloud9_region>` in the |AWS-gr|.

   .. image:: images/console-region.png
      :alt: AWS Region selector in the AWS Cloud9 console

#. If a welcome page is displayed, for :guilabel:`New AWS Cloud9 environment`, choose :guilabel:`Create environment`.
   Otherwise, choose :guilabel:`Create environment`.

   .. image:: images/console-welcome-new-env.png
      :alt: Welcome page in the AWS Cloud9 console

   Or:
   
   .. image:: images/console-new-env.png
      :alt: Create environment button in the AWS Cloud9 console

#. On the :guilabel:`Name environment` page, for :guilabel:`Name`, type a name for your |env|.

   In this tutorial, we use the name :code:`my-demo-environment`.
   If you use a different |env| name, substitute it throughout this tutorial.

#. For :guilabel:`Description`, type something about your |env|. For example, :code:`This environment is for the AWS Cloud9 tutorial.`
#. Choose :guilabel:`Next step`.
#. On the :guilabel:`Configure settings` page, for :guilabel:`Environment type`, leave the default choice of
   :guilabel:`Create a new instance for environment (EC2)`.

   Choosing :guilabel:`Create a new instance for enviroment (EC2)` means you want |AC9| to connect the |env| to a newly-launched |EC2| instance. To use an existing |EC2| instance or your
   own server instead (which we call an :dfn:`SSH environment`), see
   :doc:`Creating an Environment <create-environment>`.

   .. note:: Choosing :guilabel:`Create a new instance for environment (EC2)` might result in possible charges to your AWS account for |EC2|.

#. For :guilabel:`Instance type`, leave the default choice. This choice has relatively low RAM and vCPUs, which is sufficient for this tutorial.

   .. note:: Choosing instance types with more RAM and vCPUs might result in additional charges to your AWS account for |EC2|.

#. |AC9| uses |VPClong| (|VPC|) in your AWS account to communicate with the newly-launched |EC2| instance. Depending on how |VPC| is set up in your AWS account, do one of the following.

   .. list-table::
      :widths: 2 3 1 3
      :header-rows: 1

      * - **Does the account have a VPC with at least one subnet in that VPC?**
        - **Is the VPC you want AWS Cloud9 to use the default VPC in the account?**
        - **Does the VPC have a single subnet?**
        - **Do this**
      * - No
        - |mdash|
        - |mdash|
        - If no VPC exists, create one. To do this, expand :guilabel:`Network settings`. For :guilabel:`Network (VPC)`, choose :guilabel:`Create new VPC`, and then follow the 
          on-screen directions. For more information, see :ref:`Create an Amazon VPC <vpc-settings-create-vpc>`.
          
          If a VPC exists but has no subnet, create one. To do this, expand :guilabel:`Network settings`. For :guilabel:`Network (VPC)`, choose :guilabel:`Create new subnet`, 
          and then follow the on-screen directions. For more information, see :ref:`Create a Subnet <vpc-settings-create-subnet>`.
      * - Yes
        - Yes
        - Yes
        - Skip ahead to the next step in this procedure. (|AC9| will automatically use the default VPC with its single subnet.)
      * - Yes
        - Yes
        - No
        - Expand :guilabel:`Network settings (advanced)`. For :guilabel:`Subnet`, choose the subnet you want |AC9| to use in the preselected default VPC. 
      * - Yes
        - No
        - Yes or No
        - Expand :guilabel:`Network settings`. For :guilabel:`Network (VPC)`, choose the VPC that you want |AC9| to use. 
          For :guilabel:`Subnet`, choose the subnet you want |AC9| to use in that VPC.

   For more information, see :doc:`Amazon VPC Settings <vpc-settings>`.
  
#. For :guilabel:`Cost-saving setting`, choose the amount of time after which |AC9| will stop the
   |env| after the |IDE| has not been used, or leave the default choice.

   .. note:: Choosing a shorter time period might result in fewer charges to your AWS account. Likewise, choosing a longer time might result in more charges.

#. Choose :guilabel:`Next step`.
#. On the :guilabel:`Review choices` page, choose :guilabel:`Create environment`. Wait while |AC9| creates
   your |env|. This can take several minutes. Please be patient.

After your |env| is created, the |AC9IDE| is displayed. You'll learn about the |AC9IDE| in the next
step.

To learn more about what you can do with an |env| after you finish this tutorial, see :doc:`Working with Environments <environments>`.

.. _tutorial-tour-ide:

Step 2: Tour the IDE
====================

In the previous step, you created an |env|, and the |AC9IDE| is now displayed. In this step, you'll learn how to use the |IDE|.  

The |AC9IDE| is a collection of tools you use to code, build, run, test, debug, and release software in the cloud. In this step, you experiment with the most common of these tools.
Toward the end of this tour, you use these tools to code, run, and debug your first app.

* :ref:`tutorial-menu-bar`
* :ref:`tutorial-dashboard`
* :ref:`tutorial-environment`
* :ref:`tutorial-editor`
* :ref:`tutorial-console`
* :ref:`tutorial-open-files`
* :ref:`tutorial-gutter`
* :ref:`tutorial-status-bar`
* :ref:`tutorial-navigate`
* :ref:`tutorial-commands`
* :ref:`tutorial-outline`
* :ref:`tutorial-immediate`
* :ref:`tutorial-process-list`
* :ref:`tutorial-preferences`
* :ref:`tutorial-terminal`
* :ref:`tutorial-debugger`

.. _tutorial-menu-bar:

Step 2.1: Menu Bar
------------------

The :dfn:`menu bar`, at the top edge of the IDE, contains common commands for working with files and code and changing IDE settings. You can also preview and run code from the menu bar.

You can hide the menu bar by choosing the arrow at its edge, as follows.

.. image:: images/ide-hide-menu-bar.png
   :alt: Hiding the menu bar in the AWS Cloud9 IDE

You can show the menu bar again by choosing the arrow in the middle of where the menu bar was earlier, as follows.

.. image:: images/ide-show-menu-bar.png
   :alt: Showing the menu bar again in the AWS Cloud9 IDE

You can use the IDE to work with a set of files in the next several sections in this tutorial. To set
up these files, choose :menuselection:`File, New File`.

Next, copy the following text into the :file:`Untitled1` editor tab.

.. code-block:: text

   fish.txt
   --------
   A fish is any member of a group of organisms that consist of
   all gill-bearing aquatic craniate animals that lack limbs with
   digits. They form a sister group to the tunicates, together
   forming the olfactores. Included in this definition are
   lampreys and cartilaginous and bony fish as well as various
   extinct related groups.

To save the file, choose :menuselection:`File, Save`. Name the file :file:`fish.txt`, and then choose :guilabel:`Save`.

Repeat these instructions, saving the second file as :file:`cat.txt`, with the following contents.

.. code-block:: text

   cat.txt
   -------
   The domestic cat is a small, typically furry, carnivorous mammal.
   They are often called house cats when kept as indoor pets or
   simply cats when there is no need to distinguish them from
   other felids and felines. Cats are often valued by humans for
   companionship and for their ability to hunt.

There are often several ways to do things in the IDE. For example, to hide the menu bar, instead of choosing
the arrow at its edge,
you can choose :menuselection:`View, Menu Bar`. To create a new file, instead of choosing :menuselection:`File,
New File` you can press :kbd:`Alt-N` (for Windows/Linux) or
:kbd:`Control-N` (for Apple OSX).
To reduce this tutorial's length, we only describe one way to do things. As you get more comfortable with
the IDE, feel free to experiment and figure out the way that works best for you.

.. _tutorial-dashboard:

Step 2.2: Dashboard
-------------------

The :dfn:`dashboard` gives you quick access to each of your environments. From the dashboard, you can
create, open, and change the setting for an |env|.

To open the dashboard, on the menu bar, choose :guilabel:`AWS Cloud9, Go To Your Dashboard`, as follows.

.. image:: images/ide-go-dashboard.png
   :alt: Opening the AWS Cloud9 dashboard

To view the settings for your |env|, choose the title inside of the :guilabel:`my-demo-environment` card.

To return to the IDE for your |env|, do one of the following:

* Choose your web browser's back button, and then choose :guilabel:`Open IDE` inside of the :guilabel:`my-demo-environment` card.
* In the navigation breadcrumb, choose :guilabel:`Environments`, and then choose :guilabel:`Open IDE` inside of the :guilabel:`my-demo-environment` card.

.. note:: It can take a few moments for the IDE to display again. Please be patient.

.. _tutorial-environment:

Step 2.3: |envtitle| Window
---------------------------

The :guilabel:`Environment` window shows a list of your folders and files in the |env|. You can also show different types of files, such as hidden files.

To hide the :guilabel:`Environment` window and the :guilabel:`Environment` button, choose
:menuselection:`Window, Environment` on the menu bar.

To show the :guilabel:`Environment` button again, choose :menuselection:`Window, Environment` again.

To show the :guilabel:`Environment` window, choose the :guilabel:`Environment` button.

To show hidden files, in the :guilabel:`Environment` window, choose the gear icon, and then choose :menuselection:`Show Hidden Files`, as follows.

.. image:: images/ide-show-hidden-files.png
   :alt: Showing hidden files using the Environment window

To hide hidden files, choose the gear icon again, and then choose :menuselection:`Show Hidden Files` again.

.. _tutorial-editor:

Step 2.4: Editor, Tabs, and Panes
---------------------------------

The :dfn:`editor` is where you can do things such as write code, run a terminal session, and change IDE settings. Each instance of an open file,
terminal session, and so on is represented by a :dfn:`tab`. Tabs can be grouped into :dfn:`panes`. Tabs are shown at the edge of their pane, as follows.

.. image:: images/ide-tab-buttons.png
  :alt: Tabs at the edge of a pane in the AWS Cloud9 IDE

To hide tabs, choose :menuselection:`View, Tab Buttons` on the menu bar.

To show tabs again, choose :menuselection:`View, Tab Buttons` again.

To open a new tab, choose the :guilabel:`+` icon at the edge of the row of tabs. Then choose one of the available commands, for example, :menuselection:`New File`, as follows.

.. image:: images/ide-new-file.png
   :alt: New tab with commands to choose, such as New File

To display two panes, choose the icon that looks like a drop-down menu, which is at the edge of the row of tabs. Then choose :menuselection:`Split Pane in Two Rows`, as follows.

.. image:: images/ide-split-pane-two-rows.png
   :alt: Showing two panes by splitting one pane into two rows

To return to a single pane, choose the drop-down menu icon again, and then choose the single square icon, as follows.

.. image:: images/ide-single-pane-view.png
   :alt: Showing a single pane

.. _tutorial-console:

Step 2.5: Console
-----------------

The :dfn:`console` is an alternate place for creating and managing tabs, as follows.

.. image:: images/ide-console.png
   :alt: AWS Cloud9 console

You can also change the console's display so that it takes over the entire IDE.

To hide the console, choose :menuselection:`View, Console` on the menu bar.

To show the console again, choose :menuselection:`View, Console` again.

To expand the console, choose the resize icon, which is at the edge of the console, as follows.

.. image:: images/ide-console-resize.png
   :alt: Expanding the size of the console display

To shrink the console, choose the resize icon again.

.. _tutorial-open-files:

Step 2.6: Open Files Section
----------------------------

The :guilabel:`Open Files` section shows a list of all files that are currently open in the editor. :guilabel:`Open Files` is part of the :guilabel:`Environment` window, as follows.

.. image:: images/ide-open-files.png
   :alt: Open Files section in the Environment window

To open the :guilabel:`Open Files` section, choose :menuselection:`View, Open Files` on the menu bar.

To switch between open files, choose :guilabel:`fish.txt` and then :guilabel:`cat.txt` in the :guilabel:`Open Files` section.

To hide the :guilabel:`Open Files` section, choose :menuselection:`View, Open Files` again.

.. _tutorial-gutter:

Step 2.7: Gutter
----------------

The :dfn:`gutter`, at the edge of each file in the editor, shows things like line numbers and contextual symbols as you work with files, as follows.

.. image:: images/ide-gutter.png
   :alt: Gutter in the AWS Cloud9 IDE

To hide the gutter, choose :menuselection:`View, Gutter` on the menu bar.

To show the gutter again, choose :menuselection:`View, Gutter` again.

.. _tutorial-status-bar:

Step 2.8: Status Bar
--------------------

The :dfn:`status bar`, at the edge of each file in the editor, shows things like line and character numbers, file type preference, space and tab settings, and related editor settings, as follows.

.. image:: images/ide-status-bar.png
   :alt: Status bar in the AWS Cloud9 IDE

To hide the status bar, choose :menuselection:`View, Status Bar` on the menu bar.

To show the status bar, choose :menuselection:`View, Status Bar` again.

To go to a specific line number, choose a tab such as :guilabel:`cat.txt` if it's not already selected.
Then in the status bar, choose the line and character number
(it should be something like :guilabel:`7:45`). Type a line number (like :kbd:`4`), and then press :kbd:`Enter`, as follows.

.. image:: images/ide-go-to-line.png
   :alt: Going to specific line numbers using the AWS Cloud9 status bar

To change the file type preference, in the status bar, choose a different file type. For example, for
:guilabel:`cat.txt`, choose :guilabel:`Ruby` to see the syntax colors change.
To go back to plain text colors, choose :guilabel:`Plain Text`, as follows.

.. image:: images/ide-text-color.png
   :alt: Changing file type preference in the AWS Cloud9 status bar

.. _tutorial-navigate:

Step 2.9: Navigate Window
-------------------------

The :guilabel:`Navigate` window enables you to go to a different file. To use this window, begin typing the file's name. When you see the file you want, choose it.

To hide the :guilabel:`Navigate` button, choose :menuselection:`Window, Navigate` on the menu bar.

To show the :guilabel:`Navigate` button again, choose :menuselection:`Window, Navigate` again.

To show the :guilabel:`Navigate` window, choose the :guilabel:`Navigate` button.

To go to a file, in the :guilabel:`Navigate` window, start typing the file name. For example, type :kbd:`fish`. When :guilabel:`fish.txt` is highlighted, press :kbd:`Enter`.
You can repeat this to go to a different file. For example, try going to the :file:`cat.txt` file.

.. _tutorial-commands:

Step 2.10: Commands Window
--------------------------

The :guilabel:`Commands` window enables you to find and run IDE commands. To use this window, begin typing something about the command. When you see the command you want, choose it.

To hide the :guilabel:`Commands` window and :guilabel:`Commands` button,
choose :menuselection:`Window, Commands` on the menu bar.

To show the :guilabel:`Commands` button again, choose :menuselection:`Window, Commands` again.

To show the :guilabel:`Commands` window, choose the :guilabel:`Commands` button.

For example, you can use a command to show two vertical panes in the editor. To do this, in the :guilabel:`Commands`
window, type :kbd:`split`. In the list of commands,
choose :guilabel:`twovsplit`, as follows.

.. image:: images/ide-twovsplit.png
   :alt: Showing two vertical panes in the editor

To go back to a single pane, in the :guilabel:`Commands` window, in the list of commands, choose :guilabel:`nosplit`.

.. _tutorial-outline:

Step 2.11: Outline Window
-------------------------

You can use the :guilabel:`Outline` window to quickly go to a specific file location.

To hide the :guilabel:`Outline` window and :guilabel:`Outline` button, choose :menuselection:`Window, Outline` on the menu bar.

To show the :guilabel:`Outline` button again, choose :menuselection:`Window, Outline` again.

To show the :guilabel:`Outline` window, choose the :guilabel:`Outline` button.

To see how the :guilabel:`Outline` window works, create a file named :file:`hello.rb`. Copy the following code into the file.

.. code-block:: rb

   def say_hello(i)
     puts "Hello!"
     puts "i is #{i}"
   end

   def say_goodbye(i)
     puts "i is now #{i}"
     puts "Goodbye!"
   end

   i = 1
   say_hello(i)
   i += 1
   say_goodbye(i)

Then, in the :guilabel:`Outline` window, choose :guilabel:`say_hello(i)`, and then choose :guilabel:`say_goodbye(i)`, as follows.

.. image:: images/ide-outline.png
   :alt: Outline window in AWS Cloud9 IDE

.. _tutorial-immediate:

Step 2.12: Immediate Tab
------------------------

The :guilabel:`Immediate` tab enables you to test small snippets of JavaScript code. To see how the :guilabel:`Immediate` tab works, do the following:

#. Open an :guilabel:`Immediate` tab by choosing :menuselection:`Window, New Immediate Window` on the menu bar.
#. Run some code in the :guilabel:`Immediate` tab. To try this, type the following code into the window, pressing :kbd:`Shift-Enter` after typing line 1 and again after line 2. Press :kbd:`Enter` after line 3.
   (If you press :kbd:`Enter` instead of :kbd:`Shift-Enter` after you type line 1 or line 2, the code
   will run earlier than you want it to.)

   .. code-block:: js

      for (i = 0; i <= 10; i++) { // Press Shift-Enter after typing this line.
        console.log(i)            // Press Shift-Enter after typing this line.
      }                           // Press Enter after typing this line. The numbers 0 to 10 will be printed.

   .. image:: images/ide-immediate.png
      :alt: Running code in the Immediate tab

.. _tutorial-process-list:

Step 2.13: Process List
-----------------------

The :guilabel:`Process List` shows all of the running processes. You can stop or even forcibly stop processes that you don't want to run anymore.
To see how the :guilabel:`Process List` window works, do the following:

#. Show the :guilabel:`Process List` by choosing :menuselection:`Tools, Process List` on the menu bar.
#. Find a process. In the :guilabel:`Process List`, type the name of the process.
#. Stop or forcibly stop a process. In the list of processes, choose the process, and then choose :guilabel:`Kill` or :guilabel:`Force Kill`, as follows:

.. image:: images/ide-process-list.png
   :alt: Process list in the AWS Cloud9 IDE

.. _tutorial-preferences:

Step 2.14: Preferences
----------------------

:dfn:`Preferences` include the following settings:

* Settings for the current |env| only, such as such as whether to use soft tabs in the editor, the file types to ignore, and code completion behaviors for languages such as PHP and Python.
* Your user settings across each of your environments, such as colors, fonts, and editor behaviors.
* Your keybindings, such as which shortcut key combinations you prefer to use to work with files and the editor.
* Which IDE plugins to load.
* The IDE's overall theme.
* Which experimental IDE features are loaded, such as custom IDE components.

To show preferences, choose :menuselection:`AWS Cloud9, Preferences` on the menu bar. The following is displayed.

.. image:: images/ide-preferences.png
   :alt: Showing preferences in the AWS Cloud9 IDE

.. _tutorial-terminal:

Step 2.15: Terminal
-------------------

You can run one or more :dfn:`terminal` sessions in the IDE. To start a terminal session, choose :menuselection:`Window, New Terminal` on the menu bar.

You can try running a command in the terminal. For example, in the terminal, type :kbd:`echo $PATH` (to print the value of the :code:`PATH` environment variable), and then press :kbd:`Enter`.

You can also try running additional commands. For example, try commands such as the following:

* :command:`pwd` to print the path to the current directory.
* :command:`aws --version` to print version information about the |cli|.
* :command:`ls -l` to print information about the current directory.

.. _tutorial-debugger:

Step 2.16: Debugger Window
--------------------------

You can use the :guilabel:`Debugger` window to debug your code. For example, you can step through running code a portion at a time, watch the values of variables
over time, and explore the call stack.

To hide the :guilabel:`Debugger` window and :guilabel:`Debugger` button, choose :menuselection:`Window, Debugger` on the menu bar.

To show the :guilabel:`Debugger` button again, choose :menuselection:`Window, Debugger` again.

To show the :guilabel:`Debugger` window, choose the :guilabel:`Debugger` button.

You can experiment with using the :guilabel:`Debugger` window and some JavaScript code. To try this, do the following:

#. Prepare to use the :guilabel:`Debugger` window to debug JavaScript code by installing Node.js into
   your |env|, if it isn't already installed. To confirm whether your |env| has Node.js installed,
   run the :command:`node --version` command. If Node.js is installed, the Node.js version number is output,
   and you can skip ahead to step 3 in this procedure to write some JavaScript code.
#. To install Node.js:

   #. Run the following two commands, one at a time, to be sure your |env| has the latest updates, and
      then download Node Version Manager (nvm). (nvm is a simple
      Bash shell script that is useful for installing and managing Node.js versions. For more information, see
      `Node Version Manager <https://github.com/creationix/nvm/blob/master/README.md>`_ on GitHub.)

      .. code-block:: sh

         sudo yum -y update
         curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash

   #. Use a text editor to update your :file:`~/.bashrc` file to enable nvm to load. For example, in the :guilabel:`Environment` window of the |IDE|, choose the gear icon, and then choose :guilabel:`Show Home in Favorites`.
      Repeat this step and choose :guilabel:`Show Hidden Files` as well.
   #. Open the :file:`~/.bashrc` file.
   #. Type or paste the following code at the end of the file to enable nvm to load.

      .. code-block:: sh

         export NVM_DIR="/home/ec2-user/.nvm"
         [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm.

   #. Save the file.
   #. Start a new terminal session, and then run this command to install the latest version of Node.js.

      .. code-block:: sh

         nvm install node

#. Write some JavaScript code to debug. For example, create a file, add the following code to the file, and save it as :file:`hello.js`.

   .. code-block:: js

      var i;

      i = 10;

      console.log("Hello!");
      console.log("i is " + i);

      i += 1;

      console.log("i is now " + i);
      console.log("Goodbye!");

#. Add some breakpoints to the code. For example, in the gutter, choose the margin next to lines 6 and
   10. A red circle is displayed next to each of these line numbers, as follows.

   .. image:: images/ide-breakpoints.png
      :alt: Adding breakpoints to code in the Debugger window

#. Now you're ready to debug the JavaScript code. To try this, do the following:

   #. Show the :guilabel:`Debugger` window, if it's not already displayed.
   #. Watch the value of the variable named :code:`i` while the code is running. In the :guilabel:`Debugger` window, for :guilabel:`Watch Expressions`, choose :guilabel:`Type an expression here`.
      Type the letter :kbd:`i`, and then press :kbd:`Enter`, as follows.

      .. image:: images/ide-watch-expression.png
         :alt: Debugger window

   #. Begin running the code. Choose :menuselection:`Run, Run With, Node.js`, as follows.

      .. image:: images/ide-run-with.png
         :alt: Debugger window

   #. The code pauses running on line 6. The :guilabel:`Debugger` window shows the value of :code:`i` in :guilabel:`Watch Expressions`, which is currently :code:`10`, as follows.

      .. image:: images/ide-breakpoint-hit.png
         :alt: Debugger window

   #. In the :guilabel:`Debugger` window, choose :guilabel:`Resume`, which is the blue arrow icon, as follows.

      .. image:: images/ide-resume.png
         :alt: Resuming debugging in the Debugger window

   #. The code pauses running on line 10. The :guilabel:`Debugger` window now shows the new value of :code:`i`, which is currently :code:`11`.
   #. Choose :guilabel:`Resume` again. The code runs to the end. The output is printed to the console's :guilabel:`hello.js` tab, as follows.

      .. image:: images/ide-debugger-output.png
         :alt: hello.js tab with debug output

.. _tutorial-clean-up:

Step 3: Clean Up
================

To prevent ongoing charges to your AWS account related to this tutorial, you should delete the |env|.

.. warning:: Deleting an |env| cannot be undone.

#. Open the dashboard. To do this, on the menu bar in the |IDE|, choose :menuselection:`AWS Cloud9, Go To Your Dashboard`.
#. Do one of the following:

   * Choose the title inside of the :guilabel:`my-demo-environment` card, and then choose :guilabel:`Delete`.

     .. image:: images/console-delete-env.png
        :alt: Deleting an environment in the environment details page 

   * Select the :guilabel:`my-demo-environment` card, and then choose :guilabel:`Delete`.

     .. image:: images/console-delete-env-card.png
        :alt: Deleting an environment in the environments list

#. In the :guilabel:`Delete` dialog box, type :kbd:`Delete`, and then choose :guilabel:`Delete`.

.. note:: If the |env| was an |envec2|, |AC9| also terminates the |EC2| instance that was connected to that |env|.

   However, if the |env| was an |envssh|, and that |env| was connected to an |EC2| instance, |AC9| doesn't terminate 
   that instance. If you don't terminate that instance later, your AWS account might continue to have ongoing charges 
   for |EC2| related to that instance.

.. _tutorial-next-steps:

Next Steps
==========

As you continue to get familiar with the |AC9IDE|, you can continue by experimenting with some of our :doc:`Samples <samples>`. Or
create a new |env| and start working on your own projects!
