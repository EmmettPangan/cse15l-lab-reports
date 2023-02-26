# Lab Report 4
By: Emmett Pangan

### Step 1. Log into ieng6
Keys pressed: `<Up><Enter>`

<img width="579" alt="image" src="https://user-images.githubusercontent.com/110417473/221388073-98e0c140-7618-45cc-9c3b-46ab4b25a507.png">

The command `ssh cs15lwi23asb@ieng6.ucsd.edu` was the last command that I had run, so using the up arrow retrieved it from the command history to be run again.

### Step 2. Clone your fork
Keys pressed: `<Ctrl+R>git clone<Enter>`

<img width="578" alt="image" src="https://user-images.githubusercontent.com/110417473/221388167-5c6ff225-57ba-44ad-bef5-211f3d161c8f.png">

I used `Ctrl+R` to reverse search my command history, which already contained the command `git clone git@github.com:EmmettPangan/lab7.git` from previous runs. Since there were other commands that began with `git` in my command history, I used a more specific reverse search of `git clone` to ensure that I was finding the correct command.

### Step 3. Run JUnit tests, demonstrating failure
Keys pressed: `cd lab7<Enter>`, `<Ctrl+R>javac<Enter>`, `<Ctrl+R>java -cp<Enter>`

<img width="582" alt="image" src="https://user-images.githubusercontent.com/110417473/221388343-4ed62e06-ab91-470f-bfef-862e059e6bb0.png">

First, I used the `cd` command to change to the repository directory called `lab7`, which would be necessary for running the following `javac` and `java` commands.

For the `javac` command, I used `Ctrl+R` to reverse search my command history, which already contained the command `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` from previous runs. Reverse searching `javac` was sufficient to find the correct command.

For the `java` command, I used `Ctrl+R` to reverse search my command history, which already contained the command `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` from previous runs. Since there were multiple commands containing the word `java` in my command history, I used a more specific reverse search of `java -cp` to ensure that I was finding the correct command.

### Step 4. Edit file to fix failing test
Keys pressed: `vim L<Tab>.java<Enter>`, `i`, (click on buggy line and type `index2` in place of `index1`), `<Esc>:wq!<Enter>`

<img width="566" alt="image" src="https://user-images.githubusercontent.com/110417473/221388676-212980de-48b1-4fd4-8b6c-4f76dc5e0529.png">

<img width="574" alt="image" src="https://user-images.githubusercontent.com/110417473/221388605-0fc8d29f-733d-4a8b-8152-723bdfb156a0.png">

To open up the buggy file to edit it, I used the command `vim` with the name of the buggy file, `ListExamples.java`. To get the file name `ListExamples.java`, I used `Tab` to complete `ListExamples` after typing in the first letter and then completing the `.java` extension manually.

In vim, typing the letter `i` enters insert mode, allowing you to edit the file.

I manually scrolled to the buggy line and changed the mixed-up variable name to the correct variable name.

To exit the file, I used `Esc` to disable insert mode and `:wq!` to write and quit the file.

### Step 5. Run JUnit tests, demonstrating success
Keys pressed: `<Up><Up><Up><Enter>`, `<Up><Up><Up><Enter>`

<img width="579" alt="image" src="https://user-images.githubusercontent.com/110417473/221388858-aa71eea0-a17f-4739-8209-59c6b5fd4bab.png">

To recompile the files, I used three up arrows to access the `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` command that was in my command history from Step 3.

Similarly, to run the files, I used three up arrows to access the `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` command that was in my command histoy from Step 3.

### Step 6. Commit and push changes to GitHub
Keys pressed: `<Ctrl+R>git add<Enter>`, `<Ctrl+R>git commit<Enter>`, `git push`

<img width="569" alt="image" src="https://user-images.githubusercontent.com/110417473/221388976-c45ffc33-f22c-4e0c-aacc-6130675cee2d.png">

To add the changed `ListExamples.java` to the commit, I used `Ctrl+R` to reverse search my command history, which contained the command `git add ListExamples.java` from previous runs. Since there were other commands that began with `git` in my command history, I used a more specific reverse search of `git add` to ensure that I was finding the correct command.

To commit the changed file, I used `Ctrl+R` to reverse search my command history, which contained the command `git commit -m "Fixed bugs"` from previous runs. Since there were other commands that began with `git` in my command history, I used a more specific reverse search of `git commit` to ensure that I was finding the correct command.

Finally, I manually typed `git push` to push the changes to my GitHub repository.
