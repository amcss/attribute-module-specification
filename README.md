# Attribute Modules for CSS - Specification

Attribute Modules (AM) is a technique for using *attributes* and their *values* rather than classes for styling HTML elements.

## Syntax
### The Prefix

All AM attributes must be prefixed in order to avoid clashing with in-built HTML attributes. For the remainder of this document, the prefix `am-` will be used, but any short string would be appropriate. If the prefix begins with `data-`, all AM attributes will be valid HTML attributes.

### Attributes

The syntax for attributes follows a similar concept to BEM.

```html
<tag am-traitName>
<tag am-BlockName>
<tag am-BlockName-ChildElement>
```

Attributes can be styled directly

```css
[am-BlockName] {
  /* Block Styles */
}
```

### Values

Values are space-separated, like classes, but have a wider range of permitted characters.

```html
<tag am-traitName="value two breakpoint:three">
<tag am-BlockName="modifier">
```

Attribute-value pairs are always styled using the space-separated attribute selector, `~=`

```css
[am-traitName~="value"] { /* styles */ }
[am-traitName~="two"] { /* styles */ }
[am-traitName~="three"] { /* styles */ }
```

## Concepts

### Traits

A collection of rules that can be mixed-and-matched. Each rule tends to have only one CSS property, and no styles targeting the attribute alone.

### Modules

Modules are similar to both Blocks and Elements in BEM. Modules correspond to *attributes*, and so the majority of the styles target the attribute directly.

### Variations

Similar to the Modifier of BEM, Variations are represented by the *value* of the attribute.
