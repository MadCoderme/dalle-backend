## 📑 Table of Contents

*   [Imports](#-import-argparseimport-base64import-osfrom-pathlib-import-Pathfrom-io-import-BytesIOimport-time)
*   [Flask App Setup](#-app-Flask-nameCORSappprint   -gt-Starting-DALL-E-Server)
*   [DALL-E Model Initialization](#from-dalle-model-import-DalleModeldalle-model-Noneparser-argparseArgumentParser-description---A-DALL-E-appparser-add-argumentport-typeint-default-8000-help---backend-portparser-add-argumentmodel_version-type---parse_arg_dalle_version-default---ModelSizeMINI-help---Mini-Mega-or-Mega_fullparser-add-argument--save_to_disk-type---parse_arg_boolean-default---False-help---Should-save-generated-images-to-diskparser-add-argument--img_format-type---strlower-default---JPEG-help---Generated-images-format-choices-['jpeg', 'png']parser-add-argument--output_dir-type---str-default---DEFAULT_IMG_OUTPUT_DIR-help---Customer-directory-for-generated-imagesnargs-parser-parse_args())
*   [API Routes](#-app-route-methods-GETdef-hello_apire