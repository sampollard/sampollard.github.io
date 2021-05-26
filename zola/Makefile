# If you're coming from a new computer, run `make init`
# Run build to generate.
# Work inside the zola directory, running zola serve for fast updates
build :
	zola build

deploy : build
	cp public/index.html ..
	cp public/robots.txt ..
	cp public/sitemap.xml ..
	cp -r public/blog ..
	cp -r public/personal ..
	cp -r public/research ..
	cp -r public/calendar ..
	cp -r public/css ..

# Run if in a clean directory
init :
	mkdir -p static
	cp -r ../assets static/
	cp -r ../css static/

git :
	git add ../blog
	git add ../personal
	git add ../research
	git add ../calendar
	git add ../css
	git add ../index.html
	git add ../robots.txt
	git add ../sitemap.xml

.PHONY: clean init build deploy
clean:
	$(RM) -r public
