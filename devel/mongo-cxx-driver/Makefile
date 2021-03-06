# Created by: Simun Mikecin <numisemis@yahoo.com>
# $FreeBSD$

PORTNAME=	mongo-cxx-driver
PORTVERSION=	1.1.2
DISTVERSIONPREFIX=legacy-
PORTREVISION=	8
CATEGORIES=	devel

MAINTAINER=	numisemis@yahoo.com
COMMENT=	MongoDB Legacy C++ Driver

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/APACHE-2.0.txt

BROKEN_SSL=	openssl-devel
BROKEN_SSL_REASON_openssl-devel=	use of undeclared identifier 'BIO_s_file_internal'
BROKEN_powerpc64=			fails to configure: Checking for C++ library boost_regex... no

LIB_DEPENDS=	libboost_system.so:devel/boost-libs

MAKE_JOBS_UNSAFE=	yes

OPTIONS_DEFINE=		SCRAM-SHA-1
OPTIONS_DEFAULT=	SCRAM-SHA-1

SCRAM-SHA-1_LIB_DEPENDS=	libsasl2.so:security/cyrus-sasl2
SCRAM-SHA-1_MAKE_ARGS=		--use-sasl-client --ssl
SCRAM-SHA-1_DESC=	SCRAM-SHA-1 authentication mechanism support.

USE_GITHUB=	yes
GH_ACCOUNT=	mongodb
GH_PROJECT=	mongo-cxx-driver

USES=		scons ssl
MAKE_ARGS=	--prefix=${STAGEDIR}${PREFIX} \
		--cc=${CC} \
		--cxx=${CXX}
USE_LDCONFIG=	yes

.include <bsd.port.mk>
