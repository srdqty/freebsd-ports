# Created by: vanilla@
# $FreeBSD$

PORTNAME=	iconv
PORTVERSION=	7
PORTREVISION=	1
CATEGORIES=	converters
MASTER_SITES=	GHC
PKGNAMEPREFIX=	${LUA_PKGNAMEPREFIX}
DISTNAME=	lua-${PORTNAME}-${PORTVERSION}

MAINTAINER=	feld@FreeBSD.org
COMMENT=	Iconv binding for Lua 5

BROKEN_aarch64=		fails to link: can't create dynamic relocation R_AARCH64_ABS64 against local symbol in readonly segment defined in iconv.lo

USES=		pkgconfig iconv lua:51

USE_GITHUB=	yes
GH_ACCOUNT=	ittner
GH_PROJECT=	lua-${PORTNAME}

PLIST_FILES=	%%LUA_MODLIBDIR%%/iconv.so
CFLAGS+=	`pkgconf --cflags lua-${LUA_VER}` -I${LOCALBASE}/include
MAKE_ARGS=	LUABIN=${LUA_CMD} CFLAGS="${CFLAGS}"
LDFLAGS=	-shared ${ICONV_LIB} -L${LOCALBASE}/lib
CFLAGS_amd64=	-fPIC

do-install:
	@${MKDIR} ${STAGEDIR}${LUA_MODLIBDIR}
	${INSTALL_LIB} ${WRKSRC}/iconv.so ${STAGEDIR}${LUA_MODLIBDIR}

.include <bsd.port.mk>
