# python 的日志

```
def initlog():
 
    import logging
 
    logger = logging.getLogger()
 
    logging.basicConfig(filename='../test.log',format='%(asctime)s %(levelname)s: %(message)s', datefmt='%Y-%m-%d %H:%M:%S')
 
    hdlr = logging.StreamHandler()
 
    logger.addHandler(hdlr)
    logger.setLevel(logging.INFO)
 
    return logger
 
logg=initlog()
 
logg.info("2011-08-09")
```
