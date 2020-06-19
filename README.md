# idn-homographs-database

This is a library for detecting and generating [IDN Homographs](https://en.wikipedia.org/wiki/IDN_homograph_attack). It is based on [ShamFinder Framework](https://arxiv.org/abs/1909.07539), a research project published on Arxiv by Mori et al. 

## Install & Use

First, download the code and install dependencies:

```shell
git clone https://github.com/FlowCrypt/idn-homographs-database.git
cd idn-homographs-database
pip install -r requirements.txt
```

With that done, we can try to detect a homograph. Let's replace the lowercase L in flowcrypt.com with the number one:

```python3
>>> import homograph
>>> homograph.homographic('flowcrypt.com', 'f1owcrypt.com')
True
```

Voila! Now let's see how the library reacts to a non-homograph:

```python3
>>> homograph.homographic('flowcrylt.com', 'flowcrypt.com')
False
```

In addition to detecting homographs, the library can also be used offensively, to generate them:

```python3
>>> homograph_generator = homograph.homographs('a.b.c')
>>> next(homograph_generator)
'à.h.o'
>>> next(homograph_generator)
'à.h.𑣎'
>>> next(homograph_generator)
'à.h.с'
```

Finally, we can look at generated homographs and select only those that are currently available for purchase:

```python
>>> homograph_generator = homograph.homographs('flowcrypt')
>>> for i in homograph_generator:
...     if homograph.check_domain_availability(i + '.com'):
...         print(i + '.com')
...         break
... 
𖼷ḹ𑣎ผoŗẙꝧť.com
```
