# Scan Multibranch Pipeline Without Build

If you click on the “Scan Multibranch Pipeline Now” link in the Jenkins dashboard to discover the new branches, by default, this will automatically trigger builds for all newly discovered branches.

In this short note i am showing how to disable automatic job triggering during SCM scanning for the new branches.

Go to the configuration settings of your multibranch pipeline and in the “Branch Sources” section click on the “Add property” and select the property, named “Suppress automatic SCM triggering“.

This will prevent Jenkins from triggering the builds every time it discovers new branches.
