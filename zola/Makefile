# If you're coming from a new computer, copy css and assets into zola/static
# before building.
build :
	zola build

deploy : build
	cp public/index.html ..
	cp public/robots.txt ..
	cp public/sitemap.xml ..
	cp -r public/blog ..
	cp -r public/personal ..
	cp -r public/css ..

.PHONY: clean
clean:
	$(RM) -r public
