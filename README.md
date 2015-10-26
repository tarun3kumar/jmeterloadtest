This is a sample load test project, demonstrating jmeter and maven integration.
Please don't execute it with more than 5 threads as it uses publicly available application

You can set up a CI build based on this project and parameterize build as -

![Parameterized CI build](http://www.awesomescreenshot.com/image/695012/6b3ff35f6b855e90be9a3116fb59e597)

And now you can provide these values from building the job - 

~[Execute CI Build](http://www.awesomescreenshot.com/image/695039/1cddf23e40cf73533781cd2c244084a3)


To execute test locally execute following command - 

```
DAPP_URL=newtours.demoaut.com -DUSERS=$USERS -DDURATION=$DURATION -DRAMPUP_PERIOD=$RAMPUP_PERIOD -DSTARTUP_DELAY=$STARTUP_DELAY verify
```
    
Replace $USERS with number of users you want to run test with. Specify required values for other parameters and execute the tests

Once test execution is over then you can browse through test results under - /target/jmeter/results/index.html directory 



