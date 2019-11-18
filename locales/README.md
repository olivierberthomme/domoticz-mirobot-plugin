
i18n procedures


# New language translation

* create directory for locale (French as an exemple) :

```
mkdir -p locales/fr/LC_MESSAGES
```
* copy translation template

```
cp locales/base.pot locales/fr/LC_MESSAGES/base.po
```
* do the translation
* create binary .mo file

```
cd locales/fr/LC_MESSAGES/
msgfmt -o base.mo base
```

# New strings to be translated

* add new strings in plugin.py with `_('new string to translate')`
* update po template

```
pygettext3 -d base -o locales/base.pot plugin.py
```
* merge modifications in po files

```
for po in locales/??/LC_MESSAGES/base.po
do
  msgmerge --update $po locales/base.pot
done
```

* translate new string
* create updated binary mo files

```
for d in locales/??/LC_MESSAGES/
do
  cd $d
  msgfmt -o base.mo base
  cd -
done
```

# Initial i18n creation

This should not be needed anymore and is here for reference.

```
mkdir -p locales/ru/LC_MESSAGES
mkdir -p locales/fr/LC_MESSAGES
# create initial template from _() calls in plugin.py
pygettext3 -d base -o locales/base.pot plugin.py
# create initial translation files
for d in locales/??/LC_MESSAGES/
do
  cp locales/base.pot $d
done
# do the translation ...
# create .mo binary files
for d in locales/??/LC_MESSAGES/
do
  cd $d
  msgfmt -o base.mo base
  cd -
done
```
