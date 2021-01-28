ARG baseImage=unityci/base:latest
#ARG editorImage=unityci/editor:2020.2.1f1-base-0
ARG editorImage=unityci/editor:2019.2.11f1-base-0

FROM $editorImage as builder

# Templates
RUN echo 'Cleaning image' \
# Remove templates
    && rm -rf /opt/unity/Editor/Data/Resources/PackageManager/ProjectTemplates/ \
    && rm -rf /opt/unity/Editor/Data/Resources/PackageManager/PackageTemplates/ \
# Remove everything except manifest from packages
    && find /opt/unity/Editor/Data/Resources/PackageManager/Editor/ \
          ! -name 'manifest.json' \
          -type f -exec rm -f {} + \
# Remove unnecessary Mono resources
    && rm -rf /opt/unity/Editor/Data/MonoBleedingEdge/lib/mono/monodoc/ \
    && rm -rf /opt/unity/Editor/Data/MonoBleedingEdge/bin-linux32 \
# SDK is not required for .NET Core
    && rm -rf /opt/unity/Editor/Data/NetCore/Sdk-* \
# We are not planning to debug in CI
    && rm -rf /opt/unity/Editor/Unity_s.debug \
# Remove playback engines
    && rm -rf /opt/unity/Editor/Data/PlaybackEngines/

###########################
#          Editor         #
###########################

FROM $baseImage

# Always put "Editor" and "modules.json" directly in $UNITY_PATH
ARG UNITY_PATH=/opt/unity
COPY --from=builder "$UNITY_PATH/" "$UNITY_PATH/"

# Alias to "unity-editor" with default params
RUN echo '#!/bin/bash\nxvfb-run -ae /dev/stdout "$UNITY_PATH/Editor/Unity" -batchmode "$@"' > /usr/bin/unity-editor \
 && chmod +x /usr/bin/unity-editor
