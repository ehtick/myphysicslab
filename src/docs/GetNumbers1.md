CSS: ./Overview_2.css
Title: Getting Numbers with VarsHistory
HTML Header: <meta name="viewport" content="width=device-width, initial-scale=1">

[myPhysicsLab Documentation](index.html)

# Getting Numbers with VarsHistory

To get numeric data from a myPhysicsLab simulation using the VarsHistory class, follow the steps below.
- See the [VarsHistory source code](https://github.com/myphysicslab/myphysicslab/blob/master/src/lab/graph/VarsHistory.js)
for details and all available options.
- For more control over the output see
[Getting Numbers with Javascript](GetNumbers2.html). 

Open the terminal window by clicking the "terminal" checkbox.

&nbsp;

<img src='TerminalWindow.jpg'>
&nbsp;

Make sure you are using the [simple-compiled](Building.html#advancedvs.simplecompile)
version of the simulation. There should be a link to the simple-compiled version on the
simulation's web page, or find it on the
[set of simple-compiled applications](https://www.myphysicslab.com/develop/build/index-en.html).

Type `help` in the command box (and hit return of course) to see available commands.

Set your desired initial conditions on the simulation. Type or paste into the Terminal
command box:

    var hist = new VarsHistory(sim.getVarsList());
    simRun.addMemo(hist); 
    hist.memorize()

To memorize the starting initial conditions, we called the `memorize()` function once
before starting the simulation.

Run the simulation as long as you want. Click the "stop" button (or use a script to
automatically stop at a certain time). In the Terminal command box type:

    hist.output() 

This will print the data in Terminal output box. 

<img src='dbl-pendulum-data.png'>

The first line contains the names of the
variables. You can then select the text, copy and paste to a spreadsheet or text file.
For example I was able to generate this graph from the Double Pendulum with a
[simple Python program](dbl-pendulum-graph.html).

<img src='dbl-pendulum-graph.png'>

&nbsp;

The default separator between numbers is the tab character. To instead use comma separated values:

    hist.setSeparator(', ');

Use `setNumberFormat` to change the number formatting function. For example to show only two decimal places

    hist.setNumberFormat((n) => n.toFixed(2));

You can use
[Javascript's Number.toExponential](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toExponential)
or one of the `myphysicslab.lab.Util` number format functions like
[Util.NF5E](https://github.com/myphysicslab/myphysicslab/blob/master/src/lab/util/Util.js#L387).
The above example uses an [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
but you can provide any function that takes one numeric argument and returns a string.  Here is an equivalent non-arrow function:

    hist.setNumberFormat(function(n) { return n.toFixed(2)});

To change which variables are sampled or their order use `setVariables`. For example:

    hist.setVariables([9,0,1,2,3])

Find the index numbers of the variables by typing the command `names` into the Terminal
command box. In the
[Double Pendulum](https://www.myphysicslab.com/develop/build/sims/pendulum/DoublePendulumApp-en.html)
simulation you would see this

    SIM_VARS.ANGLE_1;
    SIM_VARS.ANGLE_1_VELOCITY;
    SIM_VARS.ANGLE_2;
    SIM_VARS.ANGLE_2_VELOCITY;
    SIM_VARS.ACCELERATION_1;
    SIM_VARS.ACCELERATION_2;
    SIM_VARS.KINETIC_ENERGY;
    SIM_VARS.POTENTIAL_ENERGY;
    SIM_VARS.TOTAL_ENERGY;
    SIM_VARS.TIME

So variable 0 is `ANGLE_`, variable 1 is `ANGLE_1_VELOCITY`, etc. Another way to find
index numbers of variables is with the command `prettyPrint(varsList)` which in the
Double Pendulum produces

    > prettyPrint(varsList)
    VarsList{
      name_: "SIM_VARS",
      numVars: 10,
      timeIdx_: 9,
      history_: false,
      (0) ANGLE_1: 0.39270,
      (1) ANGLE_1_VELOCITY: 0.00000,
      (2) ANGLE_2: 0.00000,
      (3) ANGLE_2_VELOCITY: 0.00000,
      (4) ACCELERATION_1: -6.54247,
      (5) ACCELERATION_2: 6.04446,
      (6) KINETIC_ENERGY: 0.00000,
      (7) POTENTIAL_ENERGY: 2.98392,
      (8) TOTAL_ENERGY: 2.98392,
      (9) TIME: 0.00000,



&nbsp;

&nbsp;
