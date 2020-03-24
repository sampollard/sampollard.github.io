MARKDOWN = ltac-adventures.md
HTML = $(MARKDOWN:.md=.snippet.html)

all: $(HTML)

%.snippet.html : %.md
	pandoc -f markdown -t html -o $@ $^

.PHONY : clean
clean :
	$(RM) $(HTML)
