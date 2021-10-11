DOT = dot

DOTFILES = basic_concepts
DOTSVGFLAGS := -Tsvg

all: images

images: $(DOTFILES).svg

%.svg: %.dot
	$(DOT) $(DOTSVGFLAGS) -o$@ $<
