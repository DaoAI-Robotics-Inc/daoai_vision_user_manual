Known Issues in the Jenkins System
============================================
There are some common issues that have been identified while using the Jenkins Training system.  
While they are being fixed, here is how to solve the most common ones before you feel the need to reach out for support
Please review them according to the error message output.

'Early stopping: No improvement after 5 evaluations'
-------------------------
.. image:: images/jenkins-issues-early-stopping.png
    :align: center

When the model is not improving anymore from further training the system stops the training so as not to waste time and resources.  
A common bug in Jenkins is that the program is not exited when this happens.  You may need to check periodically if you think your model is taking longer to train than expected

Fix: When you see this message, simply abort the build, and the current best model will be exported.

Resuming after Jenkins Restart
-------------------------
.. image:: images/jenkins-issues-resume.png
    :align: center

Sometimes, when Jenkins sees that the system is running slowly, it forces a restart on the system.
Unfortunately, our system is not yet set up to resume training appropriately after this.  In this case, you may see the above message.

Fix: Cancel the current training and restart it.  This message does not usually come up again, and the following training works properly.

'Mean requires at least one data point'
-------------------------

.. image:: images/jenkins-issues-mean-requires.png
    :align: center

When the dataset is too small in the system, this message appears.  It is due to the validation dataset being too small

Fix: Go to your dataset, select all the images, and copy and paste them once or twice to artificially increase the size of the dataset without needing to label more data.

'ParamScheduler RuntimeError'
-------------------------

.. image:: images/jenkins-issues-paramscheduler.png
    :align: center

This is a more uncommon error that can sometimes arise when training from a checkpoint.  It is due to the system trying to train past an expected iteration.

Fix: No easy fix for this one.  Contact a support member and tell them you have this error.