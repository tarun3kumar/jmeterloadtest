This is a sample load test project, demonstrating jmeter and maven integration.
Please don't execute it with more than 1 thread as it uses publicly available application

You can set up a CI build based on this project and parameterize build as -

![Parameterized CI build](http://www.awesomescreenshot.com/upload/18268/18496/ca7668b5-b02b-4574-6602-3154ae947aec.png)

And now you can provide these values from building the job - 

![Execute CI Build](http://www.awesomescreenshot.com/upload/18268/18496/97c57696-fc89-479e-6f47-d518fce80b49.png)


To execute test locally execute following command - 

```
DAPP_URL=newtours.demoaut.com -DUSERS=$USERS -DDURATION=$DURATION -DRAMPUP_PERIOD=$RAMPUP_PERIOD -DSTARTUP_DELAY=$STARTUP_DELAY verify
```
    
Replace $USERS with number of users you want to run test with. Specify required values for other parameters and execute the tests

Once test execution is over then you can browse through test results under - 

```
/target/jmeter/results/index.html directory
 ```



