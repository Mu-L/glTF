﻿# KHR_texture_ktx

## Contributors

* Rickard Sahlin, Ikea 
* Ben Houston, ThreeKit


Copyright (C) 2021 The Khronos Group Inc. All Rights Reserved. glTF is a trademark of The Khronos Group Inc.
See [Appendix](#appendix-full-khronos-copyright-statement) for full Khronos Copyright Statement.

## Status

Draft

## Dependencies

Written against the glTF 2.0 spec.

## Overview

This extension adds the ability to specify textures using KTX v2 images.  
An implementation of this extension can use such images as an alternative to the PNG or JPEG images available in glTF 2.0 when higher precision or range is needed.  

When the extension is used, it's allowed to use value `image/ktx2` for the `mimeType` property of images that are referenced by the `source` property of `KHR_texture_ktx` texture extension object.


## glTF Schema Updates

The `KHR_texture_ktx` extension is added to the `textures` object and specifies a `source` property that points to the index of the `image` which defines a reference to the KTX v2 image.

The following glTF will load `image.ktx2`

```json
{
    "asset": {
        "version": "2.0"
    },
    "extensionsUsed": [
        "KHR_texture_ktx"
    ],
    "textures": [
        {
            "source": 0,
            "extensions": {
                "KHR_texture_ktx": {
                    "source": 1
                }
            }
        }
    ],
    "images": [
        {
            "uri": "image.png"
        },
        {
            "uri": "image.ktx2"
        }
    ]
}
```

When used in the glTF Binary (GLB) format the `image` that points to the KTX v2 resource uses the `mimeType` value of `image/ktx2`.

```json
{
    "asset": {
        "version": "2.0"
    },
    "extensionsUsed": [
        "KHR_texture_ktx"
    ],
    "textures": [
        {
            "source": 0,
            "extensions": {
                "KHR_texture_ktx": {
                    "source": 1
                }
            }
        }
    ],
    "images": [
        {
            "mimeType": "image/png",
            "bufferView": 1
        },
        {
            "mimeType": "image/ktx2",
            "bufferView": 2
        }
    ]
}
```

### Using Without a Fallback

To use KTX v2 image without a fallback, define `KHR_texture_ktx` in both `extensionsUsed` and `extensionsRequired`. The `texture` object will then have its `source` property omitted as shown below.

```json
{
    "asset": {
        "version": "2.0"
    },
    "extensionsUsed": [
        "KHR_texture_ktx"
    ],
    "extensionsRequired": [
        "KHR_texture_ktx"
    ],
    "textures": [
        {
            "extensions": {
                "KHR_texture_ktx": {
                    "source": 0
                }
            }
        }
    ],
    "images": [
        {
            "uri": "image.ktx2"
        }
    ]
}
```

### JSON Schema

[texture.KHR_texture_ktx.schema.json](schema/texture.KHR_texture_ktx.schema.json)

## KTX v2 Images



For the purposes of this extension, the following texture types and formats are defined:

- **RGBA:** A texture that uses all four channels.  

VK_FORMAT_R16G16B16A16_SFLOAT  
VK_FORMAT_R16G16B16A16_UNORM  
VK_FORMAT_R32G32B32A32_SFLOAT  


- **RGB:** A texture that uses red, green, and blue channels. Alpha channel is unused and not sampled at runtime.  

VK_FORMAT_R16G16B16_SFLOAT  
VK_FORMAT_R16G16B16_UNORM  
VK_FORMAT_R32G32B32_SFLOAT  

- **Red:** A texture that uses only red channel. All other channels are unused and their values are not sampled at runtime.  

VK_FORMAT_R16_SFLOAT  
VK_FORMAT_R16_UNORM  
VK_FORMAT_R32_SFLOAT  

## KTX header fields

- vkFormat must be one of:  
VK_FORMAT_R16G16B16A16_SFLOAT  
VK_FORMAT_R16G16B16A16_UNORM  
VK_FORMAT_R32G32B32A32_SFLOAT  
VK_FORMAT_R16G16B16_SFLOAT  
VK_FORMAT_R16G16B16_UNORM  
VK_FORMAT_R32G32B32_SFLOAT  
VK_FORMAT_R16_SFLOAT  
VK_FORMAT_R16_UNORM  
VK_FORMAT_R32_SFLOAT  



### Additional requirements

Regardless of the format used, these additional restrictions apply for compatibility reasons:

- Swizzling metadata (`KTXswizzle`) MUST be `rgba` or omitted.
- Orientation metadata (`KTXorientation`) MUST be `rd` or omitted.


## Known Implementations

Authoring:


Viewing:


## Resources

[KTX File Format Specification, version 2](https://github.khronos.org/KTX-Specification/)

[KTX Reference Software](https://github.com/KhronosGroup/KTX-Software/)

## Appendix: Full Khronos Copyright Statement

Copyright 202§ The Khronos Group Inc.

Some parts of this Specification are purely informative and do not define requirements
necessary for compliance and so are outside the Scope of this Specification. These
parts of the Specification are marked as being non-normative, or identified as
**Implementation Notes**.

Where this Specification includes normative references to external documents, only the
specifically identified sections and functionality of those external documents are in
Scope. Requirements defined by external documents not created by Khronos may contain
contributions from non-members of Khronos not covered by the Khronos Intellectual
Property Rights Policy.

This specification is protected by copyright laws and contains material proprietary
to Khronos. Except as described by these terms, it or any components
may not be reproduced, republished, distributed, transmitted, displayed, broadcast
or otherwise exploited in any manner without the express prior written permission
of Khronos.

This specification has been created under the Khronos Intellectual Property Rights
Policy, which is Attachment A of the Khronos Group Membership Agreement available at
www.khronos.org/files/member_agreement.pdf. Khronos grants a conditional
copyright license to use and reproduce the unmodified specification for any purpose,
without fee or royalty, EXCEPT no licenses to any patent, trademark or other
intellectual property rights are granted under these terms. Parties desiring to
implement the specification and make use of Khronos trademarks in relation to that
implementation, and receive reciprocal patent license protection under the Khronos
IP Policy must become Adopters and confirm the implementation as conformant under
the process defined by Khronos for this specification;
see https://www.khronos.org/adopters.

Khronos makes no, and expressly disclaims any, representations or warranties,
express or implied, regarding this specification, including, without limitation:
merchantability, fitness for a particular purpose, non-infringement of any
intellectual property, correctness, accuracy, completeness, timeliness, and
reliability. Under no circumstances will Khronos, or any of its Promoters,
Contributors or Members, or their respective partners, officers, directors,
employees, agents or representatives be liable for any damages, whether direct,
indirect, special or consequential damages for lost revenues, lost profits, or
otherwise, arising from or in connection with these materials.

Khronos® and Vulkan® are registered trademarks, and ANARI™, WebGL™, glTF™, NNEF™, OpenVX™,
SPIR™, SPIR-V™, SYCL™, OpenVG™ and 3D Commerce™ are trademarks of The Khronos Group Inc.
OpenXR™ is a trademark owned by The Khronos Group Inc. and is registered as a trademark in
China, the European Union, Japan and the United Kingdom. OpenCL™ is a trademark of Apple Inc.
and OpenGL® is a registered trademark and the OpenGL ES™ and OpenGL SC™ logos are trademarks
of Hewlett Packard Enterprise used under license by Khronos. ASTC is a trademark of
ARM Holdings PLC. All other product names, trademarks, and/or company names are used solely
for identification and belong to their respective owners.