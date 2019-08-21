[![GoDoc](http://godoc.org/github.com/robfig/cron?status.png)](http://godoc.org/github.com/robfig/cron) 
[![Build Status](https://travis-ci.org/robfig/cron.svg?branch=master)](https://travis-ci.org/robfig/cron)

# cron

eg:
```$xslt
func StartJob() {
    c := cron.New()
    c.Start()
    _ = c.AddFunc("halfHour", "*/5 * * * * *", func() { fmt.Println("Every hour on the half hour", time.Now().Unix()) })
    _ = c.AddFunc("everyHour", "*/2 * * * * *", func() { fmt.Println("Every hour",time.Now().Unix()) })
    _ = c.AddFunc("hour","*/3 * * * * *", func() { fmt.Println("Every hour thirty", time.Now().Unix()) })
    
    fmt.Println(c.Entries())
    time.Sleep(3* time.Second)
    
    // delete job
    c.RemoveJob("everyHour")
    // Funcs are invoked in their own goroutine, asynchronously.
    
    // Funcs may also be added to a running Cron
    e := c.AddFunc("everyDay", "*/2 * * * * *", func() { fmt.Println("Every day",time.Now().Unix()) })
    fmt.Println(e)
    // Inspect the cron Job entries' next and previous run times.
    fmt.Println(c.Entries())
    
   // c.Stop()  // Stop the scheduler (does not stop any jobs already running).
    
}
```

Documentation here: https://godoc.org/github.com/robfig/cron
