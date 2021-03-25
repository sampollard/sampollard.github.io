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
	cp -r public/css ..
	cp -r 

# Run if in a clean directory
init :
	mkdir -p static
	cp -r ../assets static/
	cp -r ../css static/

.PHONY: clean init build deploy
clean:
	$(RM) -r public
