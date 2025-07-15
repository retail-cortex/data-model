# Copyright 2022 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
load("@rules_hugo//hugo:rules.bzl", "hugo_serve", "hugo_site", "hugo_theme")
load("//:build/copy_file_groups.bzl", "copy_file_groups")

hugo_theme(
    name = "hugo_theme_geekdoc",
    srcs = [
        "@hugo_theme_geekdoc//:files",
    ],
    theme_name = "hugo_theme_geekdoc",
)

copy_file_groups(
    name = "copy_api_docs",
    srcs = ["//api:api_documents"],
    prefix = "$(RULEDIR)/content/en/model",
)

hugo_site(
    name = "docs",
    assets = glob(["assets/**"]),
    config_dir = glob(["config/**"]),
    content = glob(["content/**"]) + [":copy_api_docs"],
    data = glob(["data/**"]),
    images = glob(["images/**"]),
    quiet = False,
    static = glob(["static/**"]),
    theme = ":hugo_theme_geekdoc",
    verbose = True,
)

# Run local development server
hugo_serve(
    name = "serve",
    dep = [":docs"],
)
