# $FreeBSD$

PORTNAME=	gitlab-runner
PORTVERSION=	11.0.0
CATEGORIES=	devel
MASTER_SITES=	\
		https://gitlab-runner-downloads.s3.amazonaws.com/master/docker/:dockerx64 \
		https://gitlab-runner-downloads.s3.amazonaws.com/master/docker/:dockerarm
DISTFILES=	\
		prebuilt-x86_64.tar.xz:dockerx64 \
		prebuilt-arm.tar.xz:dockerarm
DIST_SUBDIR=	gitlab-runner
EXTRACT_ONLY=	${DISTNAME}${EXTRACT_SUFX}

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Official GitLab Runner written in Go

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	go:lang/go \
		go-bindata:devel/go-bindata
RUN_DEPENDS=	ca_root_nss>=0:security/ca_root_nss \
		bash:shells/bash \
		git:devel/git

USE_GITLAB=	yes
GL_ACCOUNT=	gitlab-org
GL_COMMIT=	5396d320cd17c02bd4133d52b8ac9acd21b20f51
GITREV=		5396d320
GITBRANCH=	11-0-stable
BUILT=		2018-06-22T11:03:39+00:00

GO_LDFLAGS=	-X gitlab.com/gitlab-org/gitlab-runner/common.VERSION=${PORTVERSION} \
		-X gitlab.com/gitlab-org/gitlab-runner/common.REVISION=${GITREV} \
		-X gitlab.com/gitlab-org/gitlab-runner/common.BUILT=${BUILT} \
		-X gitlab.com/gitlab-org/gitlab-runner/common.BRANCH=${GITBRANCH} \
		-s -w

PLIST_FILES=	bin/gitlab-runner

USE_RC_SUBR=	gitlab_runner

USERS=		gitlab-runner
GROUPS=		gitlab-runner

post-extract:
	@${MKDIR} ${WRKSRC}/out/docker/
	@${CP} ${DISTDIR}/${DIST_SUBDIR}/prebuilt-x86_64.tar.xz ${WRKSRC}/out/docker/
	@${CP} ${DISTDIR}/${DIST_SUBDIR}/prebuilt-arm.tar.xz ${WRKSRC}/out/docker/

do-build:
	@cd ${WRKSRC} && go-bindata \
		-pkg docker \
		-nocompress \
		-nomemcopy \
		-nometadata \
		-prefix out/docker/ \
		-o executors/docker/bindata.go \
		out/docker/prebuilt-x86_64.tar.xz \
		out/docker/prebuilt-arm.tar.xz
	@cd ${WRKSRC} && go fmt executors/docker/bindata.go
	@${MV} ${WRKSRC}/vendor ${WRKSRC}/src
	@${MKDIR} ${WRKSRC}/src/gitlab.com/gitlab-org
	@${LN} -s ${WRKSRC} ${WRKSRC}/src/gitlab.com/gitlab-org/gitlab-runner
	@cd ${WRKSRC} && \
		${SETENV} ${MAKE_ENV} CGO_ENABLED=0 GOPATH=${WRKSRC} go build \
			-ldflags="${GO_LDFLAGS}" \
			-o gitlab-runner

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/gitlab-runner ${STAGEDIR}${PREFIX}/bin/gitlab-runner

.include <bsd.port.mk>
