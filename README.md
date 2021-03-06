localturk
=========

Local Turk implements Amazon's Mechanical Turk API on your own machine.

It's handy if you want to:

1. Develop a Mechanical Turk template
2. Do some repetitive tasks on your own, without involving Turkers.

You could use it, for instance, to generate test and training data for a Machine Learning algorithm.


Quick Start
-----------

Run:

    npm install express commander csv
    git clone https://github.com/danvk/localturk.git
    cd localturk/sample
    ../localturk.js --static_dir . transcribe.html tasks.csv outputs.csv

Then visit http://localhost:4321/ to start Turking.


Templates and Tasks
-------------------

Using Local Turk is just like using Amazon's Mechanical Turk. You create:

1. An HTML template file with a &lt;form&gt;
2. A CSV file of tasks

For example, say you wanted to record whether some images contained a red ball. You would make a CSV file containing the URLs for each image:

    image_url
    http://example.com/image_with_red_ball.png
    http://example.com/image_without_red_ball.png

Then you'd make an HTML template for the task:

```html
<img src="${image_url}" />
<input type=radio name=has_button value="yes" /> Has a red ball<br/>
<input type=radio name=has_button value="no" /> Does not have a red ball<br/>
```

Finally, you'd start up the Local Turk server:

    $ node localturk.js path/to/template.html path/to/tasks.csv path/to/output.csv

Now you can visit http://localhost:4321/ to complete each task. When you're done, the output.csv file will contain

    image_url,has_button
    http://example.com/image_with_red_ball.png,yes
    http://example.com/image_without_red_ball.png,no

