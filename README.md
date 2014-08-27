# Attribute Modules for CSS - Specification

Attribute Modules (AM) is a technique for using *attributes* and their *values* rather than classes for styling HTML elements.

## Concepts

Like other CSS methodologies, AM makes some suggestions about logical groupings for your styling code. These are Modules, Variations & Traits.

### Modules

Modules are similar to both Blocks and Elements in BEM, and can initially be considered a direct replacement for HTML classes. Modules are described by HTML *attributes*.

### Variations

Similar to the Modifier of BEM, Variations are represented by the *value* of the attribute, and extend or override the base Module's styles.

### Traits

A collection of single-purpose *values*, grouped into a namespace by the *attribute*. For example, a collection of typographical styles might be grouped into a `type` trait. This is similar to SuitCSS' [utils](https://github.com/suitcss/utils) project.

## HTML Syntax
### The Prefix

All AM attributes must be prefixed in order to avoid clashing with in-built HTML attributes. For the remainder of this document, the prefix `am-` will be used, but any short string would be appropriate. If the prefix begins with `data-`, all AM attributes will be valid HTML attributes. Here is an example of AM markup in HTML:

```html
<tag am-traitName="one two breakpoint:three">
<tag am-BlockName>
<tag am-BlockName-ChildElement>
<tag am-BlockName="variant">
```

### Attributes

The syntax for attributes follows a similar concept to Suit & BEM, with lower-camel-case names for Traits and upper-camel-case (or Pascal case) for Modules, joined by a hyphen to represent parent-child relationships.

### Values

Values are space-separated, like classes, but have a wider range of permitted characters. This is one area where AM provides you extra flexibility, so feel free to experiment.

## CSS Syntax

Attribute-value pairs are always styled using the space-separated attribute selector, `~=`. This gives precisely the same behaviour as using classes, but each attribute effectively declares its own *namespace*, affording greater flexibility & isolation in grouping your styles. Here is an example of AM syntax in CSS.

```css
[am-traitName~="value"] { /* styles */ }
[am-traitName~="two"] { /* styles */ }
[am-traitName~="three"] { /* styles */ }

[am-BlockName] {
  /* Block Styles */
}
[am-BlockName~="modifier"] {
  /* Variant Styles */
}

[am-BlockName-ChildElement] {
  /* Child Block Styles */
}
```

