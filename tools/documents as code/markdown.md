# Markdown Syntax examples

[Microsoft Docs](https://docs.microsoft.com/en-us/contribute/how-to-write-use-markdown)

> Note:
>
> Try Markdown Extended VS Code plugin for Blockquote support, table editing, etc

# This is heading 1
## This is heading 2

> The drought had lasted now for ten million years, and the reign of the terrible lizards had long since ended. Here on the Equator, in the continent which would one day be known as Africa, the battle for existence had reached a new climax of ferocity, and the victor was not yet in sight. In this barren and desiccated land, only the small or the swift or the fierce could flourish, or even hope to survive.

> Block combined with other markdown
>
> - test
>
> | x | x |
> | --- | --- |
> | x | x |

- List item 1
  - List item A
  - List item B
- List item 2
- [ ] List item 3 (check box)
- [x] List item 4 (check box)

1. First instruction
   1. Sub-instruction
   1. Sub-instruction
1. Second instruction

| Fun                  | With                 | Tables          |
| :------------------- | -------------------: |:---------------:|
| left-aligned column  | right-aligned column | centered column |
| $100                 | $100                 | $100            |
| $10                  | $10                  | $10             |
| $1                   | $1                   | $1              |

[link text](file-name.md)

[link text via reference][1]

Divider
***

```sql
CREATE TABLE T1 (
  c1 int PRIMARY KEY,
  c2 varchar(50) SPARSE NULL
);
```

![ADextension\_2FA\_Configure\_Step4](./media/bogusfilename/ADextension_2FA_Configure_Step4.PNG)

## Microsoft Open Publishing System Extended Syntax

> [!NOTE]
> This is a NOTE

> [!WARNING]
> This is a WARNING

> [!TIP]
> This is a TIP

> [!IMPORTANT]
> This is IMPORTANT

[!INCLUDE[sample include file](../includes/sampleinclude.md)]


> [!div class="op_single_selector"]
- [macOS](../docs/core/tutorials/using-on-macos.md)
- [Windows](../docs/core/tutorials/with-visual-studio.md)

[1]: file-name.md
