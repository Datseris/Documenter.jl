MAKEFILE_DIR:=$(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))

# All source files that are theme-independent
SRC_FILES =
SRC_FILES += $(wildcard scss/documenter/*.scss)
SRC_FILES += $(shell find scss/bulma/ -type f -name '*.sass')

# Compile all themes
catppuccin: themes/catppuccin-latte.css themes/catppuccin-frappe.css \
		themes/catppuccin-macchiato.css themes/catppuccin-mocha.css

# Template the flavor
scss/catppuccin-%.scss: scss/catppuccin.scss
	CATPPUCCIN_FLAVOR=$* envsubst '$${CATPPUCCIN_FLAVOR}' < $< > $@

# Compile the themes
themes/catppuccin-%.css: scss/catppuccin-%.scss scss/catppuccin/_%.scss \
		scss/catppuccin/_overrides.scss scss/catppuccin/_variables.scss \
		scss/highlightjs/catppuccin.scss $(SRC_FILES)
	julia -e 'using DocumenterTools; DocumenterTools.Themes.compile("${MAKEFILE_DIR}/$<", "${MAKEFILE_DIR}/$@")'

print-%:
	@echo '$*=$(subst ','\'',$($*))'
